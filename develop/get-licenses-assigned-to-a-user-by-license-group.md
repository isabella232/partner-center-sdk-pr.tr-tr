---
title: Lisans grubuna göre bir kullanıcıya atanan lisansları alma
description: Belirtilen lisans grupları için kullanıcı tarafından atanan lisansların listesini nasıl elde ekleyebilirsiniz?
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 54acf6f315e3062d03903a98d0c6c1946065f95e
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446012"
---
# <a name="get-licenses-assigned-to-a-user-by-license-group"></a><span data-ttu-id="d6b3e-103">Lisans grubuna göre bir kullanıcıya atanan lisansları alma</span><span class="sxs-lookup"><span data-stu-id="d6b3e-103">Get licenses assigned to a user by license group</span></span>

<span data-ttu-id="d6b3e-104">Belirtilen lisans grupları için kullanıcı tarafından atanan lisansların listesini nasıl elde ekleyebilirsiniz?</span><span class="sxs-lookup"><span data-stu-id="d6b3e-104">How to get a list of user assigned licenses for the specified license groups.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d6b3e-105">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="d6b3e-105">Prerequisites</span></span>

- <span data-ttu-id="d6b3e-106">kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="d6b3e-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="d6b3e-107">Bu senaryo yalnızca App+User kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="d6b3e-107">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="d6b3e-108">Müşteri kimliği ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="d6b3e-108">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="d6b3e-109">Müşterinin kimliğini bilmiyorsanız bu kimliği panoda [İş Ortağı Merkezi.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="d6b3e-109">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="d6b3e-110">İş Ortağı Merkezi **menüsünden CSP'yi** ve ardından **Müşteriler'i seçin.**</span><span class="sxs-lookup"><span data-stu-id="d6b3e-110">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="d6b3e-111">Müşteri listesinden müşteriyi ve ardından Hesap'ı **seçin.**</span><span class="sxs-lookup"><span data-stu-id="d6b3e-111">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="d6b3e-112">Müşterinin Hesap sayfasında Müşteri Hesabı Bilgileri **bölümünde Microsoft** **Kimliği'ne** bakın.</span><span class="sxs-lookup"><span data-stu-id="d6b3e-112">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="d6b3e-113">Microsoft Kimliği, müşteri kimliği () ile `customer-tenant-id` aynıdır.</span><span class="sxs-lookup"><span data-stu-id="d6b3e-113">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="d6b3e-114">Bir kullanıcı tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="d6b3e-114">A user identifier.</span></span>

- <span data-ttu-id="d6b3e-115">Bir veya daha fazla lisans grubu tanımlayıcısının listesi.</span><span class="sxs-lookup"><span data-stu-id="d6b3e-115">A list of one or more license group identifiers.</span></span>

## <a name="c"></a><span data-ttu-id="d6b3e-116">C\#</span><span class="sxs-lookup"><span data-stu-id="d6b3e-116">C\#</span></span>

<span data-ttu-id="d6b3e-117">Bir kullanıcıya belirtilen lisans gruplarından hangi lisansların atandığı kontrol etmek için, [**licenseGroupId**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licensegroupid)türünde bir [List/dotnet/api/system.collections.generic.list-1) örneği başlatarak ve ardından lisans gruplarını listeye ekleyin.</span><span class="sxs-lookup"><span data-stu-id="d6b3e-117">To check which licenses are assigned to a user from specified license groups, start by instantiating a [List/dotnet/api/system.collections.generic.list-1) of type [**LicenseGroupId**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licensegroupid), and then add the license groups to the list.</span></span> <span data-ttu-id="d6b3e-118">Ardından, müşteriyi [**tanımlamak için IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini müşteri kimliğiyle birlikte kullanın.</span><span class="sxs-lookup"><span data-stu-id="d6b3e-118">Then, use the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="d6b3e-119">Ardından, kullanıcı kimliğini [**belirlemek için Users.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) yöntemini çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d6b3e-119">Next, call the [**Users.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method with the user ID to identify the user.</span></span> <span data-ttu-id="d6b3e-120">Ardından, Lisanslar özelliğinden müşteri kullanıcı lisans işlemlerine [**bir arabirim**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.licenses) alın.</span><span class="sxs-lookup"><span data-stu-id="d6b3e-120">Then, get an interface to customer user license operations from the [**Licenses**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.licenses) property.</span></span> <span data-ttu-id="d6b3e-121">Son olarak, kullanıcıya atanmış lisans koleksiyonunu almak için lisans gruplarının listesini [**Get**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicensecollection.get) veya [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicensecollection.getasync) yöntemine iletirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d6b3e-121">Finally, pass the list of license groups to the [**Get**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicensecollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicensecollection.getasync) method to retrieve the collection of licenses assigned to the user.</span></span>

``` csharp
// string selectedCustomerUserId;
// string selectedCustomerId;
// IAggregatePartner partnerOperations;

// To get the group1 (Azure Active Directory (AAD)) assigned licenses.
List<LicenseGroupId> licenseGroupIds = new List<LicenseGroupId>(){ LicenseGroupId.Group1 };
var customerUserAadAssignedLicenses = partnerOperations.Customers.ById(selectedCustomerId).Users.ById(selectedCustomerUserId).Licenses.Get(licenseGroupIds);

// To get the group2 (Minecraft) assigned licenses.
List<LicenseGroupId> licenseGroupIds = new List<LicenseGroupId>(){ LicenseGroupId.Group2 };
var customerUserSfbAssignedLicenses = partnerOperations.Customers.ById(selectedCustomerId).Users.ById(selectedCustomerUserId).Licenses.Get(licenseGroupIds);

// To get both AAD and Minecraft assigned licenses.
List<LicenseGroupId> licenseGroupIds = new List<LicenseGroupId>(){ LicenseGroupId.Group1, LicenseGroupId.Group2 };
var customerUserBothAadAndSfbAssignedLicenses = partnerOperations.Customers.ById(selectedCustomerId).Users.ById(selectedCustomerUserId).Licenses.Get(licenseGroupIds);
```

## <a name="rest-request"></a><span data-ttu-id="d6b3e-122">REST isteği</span><span class="sxs-lookup"><span data-stu-id="d6b3e-122">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="d6b3e-123">İstek söz dizimi</span><span class="sxs-lookup"><span data-stu-id="d6b3e-123">Request syntax</span></span>

| <span data-ttu-id="d6b3e-124">Yöntem</span><span class="sxs-lookup"><span data-stu-id="d6b3e-124">Method</span></span>  | <span data-ttu-id="d6b3e-125">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="d6b3e-125">Request URI</span></span>                                                                                                                                            |
|---------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="d6b3e-126">**Al**</span><span class="sxs-lookup"><span data-stu-id="d6b3e-126">**GET**</span></span> | <span data-ttu-id="d6b3e-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/users/{user-id}/licenses?licenseGroupIds=Group1 HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="d6b3e-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/users/{user-id}/licenses?licenseGroupIds=Group1 HTTP/1.1</span></span>                        |
| <span data-ttu-id="d6b3e-128">**Al**</span><span class="sxs-lookup"><span data-stu-id="d6b3e-128">**GET**</span></span> | <span data-ttu-id="d6b3e-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/users/{user-id}/licenses?licenseGroupIds=Group2 HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="d6b3e-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/users/{user-id}/licenses?licenseGroupIds=Group2 HTTP/1.1</span></span>                        |
| <span data-ttu-id="d6b3e-130">**Al**</span><span class="sxs-lookup"><span data-stu-id="d6b3e-130">**GET**</span></span> | <span data-ttu-id="d6b3e-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/users/{user-id}/licenses?licenseGroupIds=Group1&licenseGroupIds=Group2 HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="d6b3e-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/users/{user-id}/licenses?licenseGroupIds=Group1&licenseGroupIds=Group2 HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="d6b3e-132">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="d6b3e-132">URI parameter</span></span>

<span data-ttu-id="d6b3e-133">Müşteri, kullanıcı ve lisans gruplarını tanımlamak için aşağıdaki yolu ve sorgu parametrelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="d6b3e-133">Use the following path and query parameters to identify the customer, user, and license groups.</span></span>

| <span data-ttu-id="d6b3e-134">Ad</span><span class="sxs-lookup"><span data-stu-id="d6b3e-134">Name</span></span>            | <span data-ttu-id="d6b3e-135">Tür</span><span class="sxs-lookup"><span data-stu-id="d6b3e-135">Type</span></span>   | <span data-ttu-id="d6b3e-136">Gerekli</span><span class="sxs-lookup"><span data-stu-id="d6b3e-136">Required</span></span> | <span data-ttu-id="d6b3e-137">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d6b3e-137">Description</span></span>                                                                                                                                                                                                                                                           |
|-----------------|--------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="d6b3e-138">customer-id</span><span class="sxs-lookup"><span data-stu-id="d6b3e-138">customer-id</span></span>     | <span data-ttu-id="d6b3e-139">string</span><span class="sxs-lookup"><span data-stu-id="d6b3e-139">string</span></span> | <span data-ttu-id="d6b3e-140">Yes</span><span class="sxs-lookup"><span data-stu-id="d6b3e-140">Yes</span></span>      | <span data-ttu-id="d6b3e-141">Müşteriyi tanımlayan GUID biçimli bir dize.</span><span class="sxs-lookup"><span data-stu-id="d6b3e-141">A GUID formatted string that identifies the customer.</span></span>                                                                                                                                                                                                                 |
| <span data-ttu-id="d6b3e-142">user-id</span><span class="sxs-lookup"><span data-stu-id="d6b3e-142">user-id</span></span>         | <span data-ttu-id="d6b3e-143">string</span><span class="sxs-lookup"><span data-stu-id="d6b3e-143">string</span></span> | <span data-ttu-id="d6b3e-144">Yes</span><span class="sxs-lookup"><span data-stu-id="d6b3e-144">Yes</span></span>      | <span data-ttu-id="d6b3e-145">Kullanıcıyı tanımlayan GUID biçimli bir dize.</span><span class="sxs-lookup"><span data-stu-id="d6b3e-145">A GUID formatted string that identifies the user.</span></span>                                                                                                                                                                                                                     |
| <span data-ttu-id="d6b3e-146">licenseGroupIds</span><span class="sxs-lookup"><span data-stu-id="d6b3e-146">licenseGroupIds</span></span> | <span data-ttu-id="d6b3e-147">dize</span><span class="sxs-lookup"><span data-stu-id="d6b3e-147">string</span></span> | <span data-ttu-id="d6b3e-148">No</span><span class="sxs-lookup"><span data-stu-id="d6b3e-148">No</span></span>       | <span data-ttu-id="d6b3e-149">Atanan lisansların lisans grubunu gösteren bir enum değeri.</span><span class="sxs-lookup"><span data-stu-id="d6b3e-149">An enum value that indicates the license group of the assigned licenses.</span></span> <span data-ttu-id="d6b3e-150">Geçerli değerler: Grup1, Grup2 Grup1 - Bu grupta lisansları Azure Active Directory (AAD) vardır.</span><span class="sxs-lookup"><span data-stu-id="d6b3e-150">Valid values: Group1, Group2 Group1 - This group has all products whose license can be managed in the Azure Active Directory (AAD).</span></span> <span data-ttu-id="d6b3e-151">Grup2 - Bu grubun yalnızca Minecraft lisansları vardır.</span><span class="sxs-lookup"><span data-stu-id="d6b3e-151">Group2 - This group has only Minecraft product licenses.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="d6b3e-152">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="d6b3e-152">Request headers</span></span>

<span data-ttu-id="d6b3e-153">Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="d6b3e-153">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="d6b3e-154">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="d6b3e-154">Request body</span></span>

<span data-ttu-id="d6b3e-155">Yok.</span><span class="sxs-lookup"><span data-stu-id="d6b3e-155">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="d6b3e-156">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="d6b3e-156">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/users/482e2152-4b49-48ec-b715-823365ce3d4c/licenses?licenseGroupIds=Group1&licenseGroupIds=Group2 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: a1d077e4-28b1-4578-b873-6d1a82fa1644
MS-CorrelationId: c8cb5a60-ae08-4afc-92f0-efc42adfa186
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="d6b3e-157">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="d6b3e-157">REST response</span></span>

<span data-ttu-id="d6b3e-158">Başarılı olursa yanıt gövdesi Lisans [kaynaklarının](license-resources.md#license) koleksiyonunu içerir.</span><span class="sxs-lookup"><span data-stu-id="d6b3e-158">If successful, the response body contains the collection of [License](license-resources.md#license) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="d6b3e-159">Yanıt başarı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="d6b3e-159">Response success and error codes</span></span>

<span data-ttu-id="d6b3e-160">Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="d6b3e-160">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="d6b3e-161">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="d6b3e-161">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="d6b3e-162">Tam liste için bkz. [İş Ortağı Merkezi kodları.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="d6b3e-162">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="d6b3e-163">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="d6b3e-163">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Type: application/json
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
MS-RequestId: b1317092-f087-471e-a637-f66523b2b94c
Date: June 24 2016 22:00:25 PST

{
    "totalCount": 2,
    "items": [{
            "servicePlans": [

            ],
            "productSku": {
                "id": "984df360-9a74-4647-8cf8-696749f6247a",
                "name": "Minecraft Education Edition Faculty",
                "skuPartNumber": "CFQ7TTC0K5DR/0002",
                "licenseGroupId": "group2"
            },
            "attributes": {
                "objectType": "License"
            }
        }, {
            "servicePlans": [{
                    "displayName": "Windows Defender Advanced Threat Protection",
                    "serviceName": "WINDEFATP",
                    "id": "871d91ec-ec1a-452b-a83f-bd76c7d770ef",
                    "capabilityStatus": "Assigned",
                    "targetType": "User"
                }, {
                    "displayName": "Windows 10 Enterprise E3",
                    "serviceName": "WIN10_PRO_ENT_SUB",
                    "id": "21b439ba-a0ca-424f-a6cc-52f954a5b111",
                    "capabilityStatus": "Assigned",
                    "targetType": "User"
                }
            ],
            "productSku": {
                "id": "1e7e1070-8ccb-4aca-b470-d7cb538cb07e",
                "name": "Windows 10 Enterprise E5",
                "skuPartNumber": "WIN_ENT_E5",
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

### <a name="response-example-no-matching-licenses-found"></a><span data-ttu-id="d6b3e-164">Yanıt örneği (eşleşen lisans bulunamadı)</span><span class="sxs-lookup"><span data-stu-id="d6b3e-164">Response example (no matching licenses found)</span></span>

<span data-ttu-id="d6b3e-165">Belirtilen lisans grupları için eşleşen lisans bulunamasa yanıt, değeri 0 olan totalCount öğesine sahip boş bir koleksiyon içerir.</span><span class="sxs-lookup"><span data-stu-id="d6b3e-165">If no matching licenses can be found for the specified license groups, the response contains an empty collection with a totalCount element whose value is 0.</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 71
Content-Type: application/json; charset=utf-8
MS-CorrelationId: c8cb5a60-ae08-4afc-92f0-efc42adfa186
MS-RequestId: a1d077e4-28b1-4578-b873-6d1a82fa1644
MS-CV: q05xrhUeDUKvhrFt.0
MS-ServerId: 030020525
Date: Fri, 09 Jun 2017 22:50:11 GMT

{
    "totalCount": 0,
    "items": [],
    "attributes": {
        "objectType": "Collection"
    }
}
```
