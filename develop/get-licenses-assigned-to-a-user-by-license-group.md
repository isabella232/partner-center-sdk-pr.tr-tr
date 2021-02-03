---
title: Lisans grubuna göre bir kullanıcıya atanan lisansları alma
description: Belirtilen lisans grupları için Kullanıcı tarafından atanan lisansların listesini alma.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 28c10e3e2acb30e4110213344959a87d4ddfcffb
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769670"
---
# <a name="get-licenses-assigned-to-a-user-by-license-group"></a><span data-ttu-id="bd9f2-103">Lisans grubuna göre bir kullanıcıya atanan lisansları alma</span><span class="sxs-lookup"><span data-stu-id="bd9f2-103">Get licenses assigned to a user by license group</span></span>

<span data-ttu-id="bd9f2-104">**Uygulama hedefi**</span><span class="sxs-lookup"><span data-stu-id="bd9f2-104">**Applies To**</span></span>

- <span data-ttu-id="bd9f2-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="bd9f2-105">Partner Center</span></span>

<span data-ttu-id="bd9f2-106">Belirtilen lisans grupları için Kullanıcı tarafından atanan lisansların listesini alma.</span><span class="sxs-lookup"><span data-stu-id="bd9f2-106">How to get a list of user assigned licenses for the specified license groups.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bd9f2-107">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="bd9f2-107">Prerequisites</span></span>

- <span data-ttu-id="bd9f2-108">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="bd9f2-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="bd9f2-109">Bu senaryo yalnızca uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="bd9f2-109">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="bd9f2-110">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="bd9f2-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="bd9f2-111">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bd9f2-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="bd9f2-112">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="bd9f2-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="bd9f2-113">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="bd9f2-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="bd9f2-114">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="bd9f2-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="bd9f2-115">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="bd9f2-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="bd9f2-116">Kullanıcı tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="bd9f2-116">A user identifier.</span></span>

- <span data-ttu-id="bd9f2-117">Bir veya daha fazla lisans grubu tanımlayıcısı listesi.</span><span class="sxs-lookup"><span data-stu-id="bd9f2-117">A list of one or more license group identifiers.</span></span>

## <a name="c"></a><span data-ttu-id="bd9f2-118">C\#</span><span class="sxs-lookup"><span data-stu-id="bd9f2-118">C\#</span></span>

<span data-ttu-id="bd9f2-119">Belirtilen lisans gruplarından bir kullanıcıya hangi lisansların atandığını denetlemek için, [**Licensegroupıd**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licensegroupid)türünde bir [list/DotNet/api/System. Collections. Generic. List -1) oluşturarak başlayın ve ardından Lisans gruplarını listeye ekleyin.</span><span class="sxs-lookup"><span data-stu-id="bd9f2-119">To check which licenses are assigned to a user from specified license groups, start by instantiating a [List/dotnet/api/system.collections.generic.list-1) of type [**LicenseGroupId**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licensegroupid), and then add the license groups to the list.</span></span> <span data-ttu-id="bd9f2-120">Ardından, müşteriyi tanımlamak için [**ıaggregatepartner. Customers. Byıd**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) YÖNTEMINI Müşteri kimliğiyle birlikte kullanın.</span><span class="sxs-lookup"><span data-stu-id="bd9f2-120">Then, use the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="bd9f2-121">Ardından, kullanıcıyı tanımlamak için Kullanıcı KIMLIĞIYLE [**Users. byıd**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="bd9f2-121">Next, call the [**Users.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method with the user ID to identify the user.</span></span> <span data-ttu-id="bd9f2-122">Ardından, [**lisanslar**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.licenses) özelliğinden müşteri Kullanıcı Lisansı işlemlerine yönelik bir arabirim alın.</span><span class="sxs-lookup"><span data-stu-id="bd9f2-122">Then, get an interface to customer user license operations from the [**Licenses**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.licenses) property.</span></span> <span data-ttu-id="bd9f2-123">Son olarak, kullanıcıya atanan lisansların koleksiyonunu almak için lisans grupları listesini [**Get**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicensecollection.get) veya [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicensecollection.getasync) yöntemine geçirin.</span><span class="sxs-lookup"><span data-stu-id="bd9f2-123">Finally, pass the list of license groups to the [**Get**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicensecollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicensecollection.getasync) method to retrieve the collection of licenses assigned to the user.</span></span>

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

## <a name="rest-request"></a><span data-ttu-id="bd9f2-124">REST isteği</span><span class="sxs-lookup"><span data-stu-id="bd9f2-124">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="bd9f2-125">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="bd9f2-125">Request syntax</span></span>

| <span data-ttu-id="bd9f2-126">Yöntem</span><span class="sxs-lookup"><span data-stu-id="bd9f2-126">Method</span></span>  | <span data-ttu-id="bd9f2-127">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="bd9f2-127">Request URI</span></span>                                                                                                                                            |
|---------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="bd9f2-128">**Al**</span><span class="sxs-lookup"><span data-stu-id="bd9f2-128">**GET**</span></span> | <span data-ttu-id="bd9f2-129">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-id}/Users/{User-ID}/lisanslar? Licensegroupıds = grup1 http/1.1</span><span class="sxs-lookup"><span data-stu-id="bd9f2-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/users/{user-id}/licenses?licenseGroupIds=Group1 HTTP/1.1</span></span>                        |
| <span data-ttu-id="bd9f2-130">**Al**</span><span class="sxs-lookup"><span data-stu-id="bd9f2-130">**GET**</span></span> | <span data-ttu-id="bd9f2-131">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-id}/Users/{User-ID}/lisanslar? Licensegroupıds = grup2 http/1.1</span><span class="sxs-lookup"><span data-stu-id="bd9f2-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/users/{user-id}/licenses?licenseGroupIds=Group2 HTTP/1.1</span></span>                        |
| <span data-ttu-id="bd9f2-132">**Al**</span><span class="sxs-lookup"><span data-stu-id="bd9f2-132">**GET**</span></span> | <span data-ttu-id="bd9f2-133">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Users/{User-ID}/lisanslar? Licensegroupıds = grup1&Licensegroupıds = grup2 http/1.1</span><span class="sxs-lookup"><span data-stu-id="bd9f2-133">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/users/{user-id}/licenses?licenseGroupIds=Group1&licenseGroupIds=Group2 HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="bd9f2-134">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="bd9f2-134">URI parameter</span></span>

<span data-ttu-id="bd9f2-135">Müşteriyi, Kullanıcı ve lisans gruplarını tanımlamak için aşağıdaki yolu ve sorgu parametrelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="bd9f2-135">Use the following path and query parameters to identify the customer, user and license groups.</span></span>

| <span data-ttu-id="bd9f2-136">Ad</span><span class="sxs-lookup"><span data-stu-id="bd9f2-136">Name</span></span>            | <span data-ttu-id="bd9f2-137">Tür</span><span class="sxs-lookup"><span data-stu-id="bd9f2-137">Type</span></span>   | <span data-ttu-id="bd9f2-138">Gerekli</span><span class="sxs-lookup"><span data-stu-id="bd9f2-138">Required</span></span> | <span data-ttu-id="bd9f2-139">Açıklama</span><span class="sxs-lookup"><span data-stu-id="bd9f2-139">Description</span></span>                                                                                                                                                                                                                                                           |
|-----------------|--------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="bd9f2-140">müşteri kimliği</span><span class="sxs-lookup"><span data-stu-id="bd9f2-140">customer-id</span></span>     | <span data-ttu-id="bd9f2-141">string</span><span class="sxs-lookup"><span data-stu-id="bd9f2-141">string</span></span> | <span data-ttu-id="bd9f2-142">Yes</span><span class="sxs-lookup"><span data-stu-id="bd9f2-142">Yes</span></span>      | <span data-ttu-id="bd9f2-143">Müşteriyi tanımlayan GUID biçimli dize.</span><span class="sxs-lookup"><span data-stu-id="bd9f2-143">A GUID formatted string that identifies the customer.</span></span>                                                                                                                                                                                                                 |
| <span data-ttu-id="bd9f2-144">user-id</span><span class="sxs-lookup"><span data-stu-id="bd9f2-144">user-id</span></span>         | <span data-ttu-id="bd9f2-145">string</span><span class="sxs-lookup"><span data-stu-id="bd9f2-145">string</span></span> | <span data-ttu-id="bd9f2-146">Yes</span><span class="sxs-lookup"><span data-stu-id="bd9f2-146">Yes</span></span>      | <span data-ttu-id="bd9f2-147">Kullanıcıyı tanımlayan GUID biçimli dize.</span><span class="sxs-lookup"><span data-stu-id="bd9f2-147">A GUID formatted string that identifies the user.</span></span>                                                                                                                                                                                                                     |
| <span data-ttu-id="bd9f2-148">Licensegroupıds</span><span class="sxs-lookup"><span data-stu-id="bd9f2-148">licenseGroupIds</span></span> | <span data-ttu-id="bd9f2-149">dize</span><span class="sxs-lookup"><span data-stu-id="bd9f2-149">string</span></span> | <span data-ttu-id="bd9f2-150">No</span><span class="sxs-lookup"><span data-stu-id="bd9f2-150">No</span></span>       | <span data-ttu-id="bd9f2-151">Atanan lisansların lisans grubunu gösteren bir sabit listesi değeri.</span><span class="sxs-lookup"><span data-stu-id="bd9f2-151">An enum value that indicates the license group of the assigned licenses.</span></span> <span data-ttu-id="bd9f2-152">Geçerli değerler: grup1, grup2 grup1-bu grubun lisansı Azure Active Directory (AAD) içinde yönetilebilecek tüm ürünler vardır.</span><span class="sxs-lookup"><span data-stu-id="bd9f2-152">Valid values: Group1, Group2 Group1 - This group has all products whose license can be managed in the Azure Active Directory (AAD).</span></span> <span data-ttu-id="bd9f2-153">Grup2-bu grup yalnızca Minecrat ürün lisanslarına sahiptir.</span><span class="sxs-lookup"><span data-stu-id="bd9f2-153">Group2 - This group has only Minecraft product licenses.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="bd9f2-154">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="bd9f2-154">Request headers</span></span>

<span data-ttu-id="bd9f2-155">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="bd9f2-155">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="bd9f2-156">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="bd9f2-156">Request body</span></span>

<span data-ttu-id="bd9f2-157">Yok.</span><span class="sxs-lookup"><span data-stu-id="bd9f2-157">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="bd9f2-158">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="bd9f2-158">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/users/482e2152-4b49-48ec-b715-823365ce3d4c/licenses?licenseGroupIds=Group1&licenseGroupIds=Group2 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: a1d077e4-28b1-4578-b873-6d1a82fa1644
MS-CorrelationId: c8cb5a60-ae08-4afc-92f0-efc42adfa186
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="bd9f2-159">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="bd9f2-159">REST response</span></span>

<span data-ttu-id="bd9f2-160">Başarılı olursa, yanıt gövdesi [Lisans](license-resources.md#license) kaynakları koleksiyonunu içerir.</span><span class="sxs-lookup"><span data-stu-id="bd9f2-160">If successful, the response body contains the collection of [License](license-resources.md#license) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="bd9f2-161">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="bd9f2-161">Response success and error codes</span></span>

<span data-ttu-id="bd9f2-162">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="bd9f2-162">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="bd9f2-163">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="bd9f2-163">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="bd9f2-164">Tam liste için bkz. [Partner Center hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="bd9f2-164">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="bd9f2-165">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="bd9f2-165">Response example</span></span>

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

### <a name="response-example-no-matching-licenses-found"></a><span data-ttu-id="bd9f2-166">Yanıt örneği (eşleşen lisans bulunamadı)</span><span class="sxs-lookup"><span data-stu-id="bd9f2-166">Response example (no matching licenses found)</span></span>

<span data-ttu-id="bd9f2-167">Belirtilen lisans grupları için eşleşen bir lisans bulunamazsa, yanıt, değeri 0 olan totalCount öğesi olan boş bir koleksiyon içerir.</span><span class="sxs-lookup"><span data-stu-id="bd9f2-167">If no matching licenses can be found for the specified license groups, the response contains an empty collection with a totalCount element whose value is 0.</span></span>

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
