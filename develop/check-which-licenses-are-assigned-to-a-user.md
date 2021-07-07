---
title: Bir kullanıcıya atanan lisansları alma
description: Bir müşteri hesabındaki bir kullanıcıya atanan lisansların listesini almak için Iş Ortağı Merkezi API 'Lerini nasıl kullanacağınızı öğrenin.
ms.date: 05/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: a51fc4493e2476107206b03be66004d030e2aa47
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/10/2021
ms.locfileid: "111974072"
---
# <a name="get-licenses-assigned-to-a-user-within-a-customer-account"></a><span data-ttu-id="4a17f-103">Müşteri hesabı içindeki bir kullanıcıya atanan lisansları al</span><span class="sxs-lookup"><span data-stu-id="4a17f-103">Get licenses assigned to a user within a customer account</span></span>

<span data-ttu-id="4a17f-104">Müşteri hesabı içindeki bir kullanıcıya atanan lisansların listesini alma.</span><span class="sxs-lookup"><span data-stu-id="4a17f-104">How to get a list of licenses assigned to a user within a customer account.</span></span> <span data-ttu-id="4a17f-105">Burada gösterilen örneklerde, Azure Active Directory tarafından yönetilen lisansları temsil eden varsayılan lisans grubu olan grup1 'ten atanan lisanslar döndürülür.</span><span class="sxs-lookup"><span data-stu-id="4a17f-105">The examples shown here return licenses assigned from group1, the default license group that represents licenses managed by Azure Active Directory.</span></span> <span data-ttu-id="4a17f-106">Belirtilen lisans gruplarından atanan lisansları almak için bkz. [lisans grubuna göre kullanıcıya atanan lisansları alın](get-licenses-assigned-to-a-user-by-license-group.md).</span><span class="sxs-lookup"><span data-stu-id="4a17f-106">To get licenses assigned from specified license groups, see [Get licenses assigned to a user by license group](get-licenses-assigned-to-a-user-by-license-group.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4a17f-107">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="4a17f-107">Prerequisites</span></span>

- <span data-ttu-id="4a17f-108">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="4a17f-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="4a17f-109">Bu senaryo yalnızca uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="4a17f-109">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="4a17f-110">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="4a17f-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="4a17f-111">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4a17f-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="4a17f-112">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="4a17f-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="4a17f-113">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="4a17f-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="4a17f-114">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="4a17f-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="4a17f-115">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="4a17f-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="4a17f-116">Kullanıcı tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="4a17f-116">A user identifier.</span></span>

## <a name="c"></a><span data-ttu-id="4a17f-117">C\#</span><span class="sxs-lookup"><span data-stu-id="4a17f-117">C\#</span></span>

<span data-ttu-id="4a17f-118">Varsayılan grup1 lisans grubundan bir kullanıcıya hangi lisansların atandığını denetlemek için, önce müşteriyi tanımlamak üzere müşteri KIMLIĞIYLE [**ıaggregatepartner. Customers. byıd**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini kullanın.</span><span class="sxs-lookup"><span data-stu-id="4a17f-118">To check which licenses are assigned to a user from the default group1 license group, first use the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="4a17f-119">Ardından kullanıcıyı tanımlamak için Kullanıcı KIMLIĞIYLE [**Users. byıd**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="4a17f-119">Then call the [**Users.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method with the user ID to identify the user.</span></span> <span data-ttu-id="4a17f-120">Ardından, [**lisanslar**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.licenses) özelliğinden müşteri Kullanıcı Lisansı işlemlerine yönelik bir arabirim alın.</span><span class="sxs-lookup"><span data-stu-id="4a17f-120">Next, get an interface to customer user license operations from the [**Licenses**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.licenses) property.</span></span> <span data-ttu-id="4a17f-121">Son olarak, kullanıcıya atanan lisansların koleksiyonunu almak için [**Get**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicensecollection.get) veya [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicensecollection.getasync) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="4a17f-121">Finally, call the [**Get**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicensecollection.get) or the [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicensecollection.getasync) method to retrieve the collection of licenses assigned to the user.</span></span>

``` csharp
// string selectedCustomerUserId;
// string selectedCustomerId;
// IAggregatePartner partnerOperations;

var customerUserAssignedLicenses = partnerOperations.Customers.ById(selectedCustomerId).Users.ById(selectedCustomerUserId).Licenses.Get();
```

<span data-ttu-id="4a17f-122">**Örnek**: [konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="4a17f-122">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="4a17f-123">**Project**: iş ortağı merkezi SDK örnekleri **sınıfı**: CustomerUserAssignedLicenses. cs</span><span class="sxs-lookup"><span data-stu-id="4a17f-123">**Project**: Partner Center SDK Samples **Class**: CustomerUserAssignedLicenses.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="4a17f-124">REST isteği</span><span class="sxs-lookup"><span data-stu-id="4a17f-124">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="4a17f-125">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="4a17f-125">Request syntax</span></span>

| <span data-ttu-id="4a17f-126">Yöntem</span><span class="sxs-lookup"><span data-stu-id="4a17f-126">Method</span></span>  | <span data-ttu-id="4a17f-127">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="4a17f-127">Request URI</span></span>                                                                                              |
|---------|----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="4a17f-128">**Al**</span><span class="sxs-lookup"><span data-stu-id="4a17f-128">**GET**</span></span> | <span data-ttu-id="4a17f-129">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Users/{User-ID}/lisanslar http/1.1</span><span class="sxs-lookup"><span data-stu-id="4a17f-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/users/{user-id}/licenses HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="4a17f-130">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="4a17f-130">URI parameter</span></span>

<span data-ttu-id="4a17f-131">Müşteriyi ve kullanıcıyı tanımlamak için aşağıdaki yol parametrelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="4a17f-131">Use the following path parameters to identify the customer and user.</span></span>

| <span data-ttu-id="4a17f-132">Ad</span><span class="sxs-lookup"><span data-stu-id="4a17f-132">Name</span></span>        | <span data-ttu-id="4a17f-133">Tür</span><span class="sxs-lookup"><span data-stu-id="4a17f-133">Type</span></span>   | <span data-ttu-id="4a17f-134">Gerekli</span><span class="sxs-lookup"><span data-stu-id="4a17f-134">Required</span></span> | <span data-ttu-id="4a17f-135">Açıklama</span><span class="sxs-lookup"><span data-stu-id="4a17f-135">Description</span></span>                                           |
|-------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="4a17f-136">müşteri kimliği</span><span class="sxs-lookup"><span data-stu-id="4a17f-136">customer-id</span></span> | <span data-ttu-id="4a17f-137">string</span><span class="sxs-lookup"><span data-stu-id="4a17f-137">string</span></span> | <span data-ttu-id="4a17f-138">Yes</span><span class="sxs-lookup"><span data-stu-id="4a17f-138">Yes</span></span>      | <span data-ttu-id="4a17f-139">Müşteriyi tanımlayan GUID biçimli dize.</span><span class="sxs-lookup"><span data-stu-id="4a17f-139">A GUID formatted string that identifies the customer.</span></span> |
| <span data-ttu-id="4a17f-140">user-id</span><span class="sxs-lookup"><span data-stu-id="4a17f-140">user-id</span></span>     | <span data-ttu-id="4a17f-141">string</span><span class="sxs-lookup"><span data-stu-id="4a17f-141">string</span></span> | <span data-ttu-id="4a17f-142">Yes</span><span class="sxs-lookup"><span data-stu-id="4a17f-142">Yes</span></span>      | <span data-ttu-id="4a17f-143">Kullanıcıyı tanımlayan GUID biçimli dize.</span><span class="sxs-lookup"><span data-stu-id="4a17f-143">A GUID formatted string that identifies the user.</span></span>     |

### <a name="request-headers"></a><span data-ttu-id="4a17f-144">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="4a17f-144">Request headers</span></span>

<span data-ttu-id="4a17f-145">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="4a17f-145">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="4a17f-146">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="4a17f-146">Request body</span></span>

<span data-ttu-id="4a17f-147">Yok.</span><span class="sxs-lookup"><span data-stu-id="4a17f-147">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="4a17f-148">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="4a17f-148">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/users/482e2152-4b49-48ec-b715-823365ce3d4c/licenses HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 68e50b00-e1ff-422a-a293-158617463d41
MS-CorrelationId: 813f15b3-eb18-4709-b2f3-668d62babf91
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="4a17f-149">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="4a17f-149">REST response</span></span>

<span data-ttu-id="4a17f-150">Başarılı olursa, yanıt gövdesi [Lisans](license-resources.md#license) kaynakları koleksiyonunu içerir.</span><span class="sxs-lookup"><span data-stu-id="4a17f-150">If successful, the response body contains the collection of [License](license-resources.md#license) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="4a17f-151">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="4a17f-151">Response success and error codes</span></span>

<span data-ttu-id="4a17f-152">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="4a17f-152">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="4a17f-153">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="4a17f-153">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="4a17f-154">Tam liste için bkz. [Partner Center hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="4a17f-154">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="4a17f-155">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="4a17f-155">Response example</span></span>

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