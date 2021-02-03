---
title: Lisans grubuna göre kullanılabilir lisansların bir listesini alma
description: Belirtilen lisans gruplarına yönelik lisansların bir listesini, belirtilen müşterinin kullanıcıları tarafından kullanılabilir.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 5092bc73107231d602c1465c8d157cdf5499c913
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769556"
---
# <a name="get-a-list-of-available-licenses-by-license-group"></a><span data-ttu-id="01541-103">Lisans grubuna göre kullanılabilir lisansların bir listesini alma</span><span class="sxs-lookup"><span data-stu-id="01541-103">Get a list of available licenses by license group</span></span>

<span data-ttu-id="01541-104">**Uygulama hedefi**</span><span class="sxs-lookup"><span data-stu-id="01541-104">**Applies To**</span></span>

- <span data-ttu-id="01541-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="01541-105">Partner Center</span></span>

<span data-ttu-id="01541-106">Belirtilen lisans gruplarına yönelik lisansların bir listesini, belirtilen müşterinin kullanıcıları tarafından kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="01541-106">How to get a list of licenses for the specified license groups available to users of the specified customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="01541-107">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="01541-107">Prerequisites</span></span>

- <span data-ttu-id="01541-108">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="01541-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="01541-109">Bu senaryo yalnızca uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="01541-109">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="01541-110">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="01541-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="01541-111">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="01541-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="01541-112">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="01541-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="01541-113">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="01541-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="01541-114">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="01541-114">On the customer's Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="01541-115">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="01541-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="01541-116">Bir veya daha fazla lisans grubu tanımlayıcısı listesi.</span><span class="sxs-lookup"><span data-stu-id="01541-116">A list of one or more license group identifiers.</span></span>

## <a name="c"></a><span data-ttu-id="01541-117">C\#</span><span class="sxs-lookup"><span data-stu-id="01541-117">C\#</span></span>

<span data-ttu-id="01541-118">Belirtilen lisans grupları için kullanılabilir lisansların bir listesini almak için, [**Licensegroupıd**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licensegroupid)türünde bir [liste](/dotnet/api/system.collections.generic.list-1) oluşturarak başlayın ve ardından Lisans gruplarını listeye ekleyin.</span><span class="sxs-lookup"><span data-stu-id="01541-118">To get a list of available licenses for the specified license groups, start by instantiating a [List](/dotnet/api/system.collections.generic.list-1) of type [**LicenseGroupId**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licensegroupid), and then add the license groups to the list.</span></span> <span data-ttu-id="01541-119">Ardından, müşteriyi tanımlamak için, müşteri KIMLIĞIYLE [**ıaggregatepartner. Customers. Byıd**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini kullanın.</span><span class="sxs-lookup"><span data-stu-id="01541-119">Next, use the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="01541-120">Ardından, müşteri abone olunan SKU toplama işlemlerine bir arabirim almak için [**SubscribedSkus**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscribedskus) özelliğinin değerini alın.</span><span class="sxs-lookup"><span data-stu-id="01541-120">Then, get the value of the [**SubscribedSkus**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscribedskus) property to retrieve an interface to customer subscribed SKU collection operations.</span></span> <span data-ttu-id="01541-121">Son olarak, abone olan SKU 'ların listesini, kullanılabilir lisans birimleri hakkındaki ayrıntılarla almak için [**Get**](/dotnet/api/microsoft.store.partnercenter.subscribedskus.icustomersubscribedskucollection.get) veya [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscribedskus.icustomersubscribedskucollection.getasync) yöntemine yönelik lisans grupları listesini geçirin.</span><span class="sxs-lookup"><span data-stu-id="01541-121">Finally, pass the list of license groups to the [**Get**](/dotnet/api/microsoft.store.partnercenter.subscribedskus.icustomersubscribedskucollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscribedskus.icustomersubscribedskucollection.getasync) method to retrieve the list of subscribed SKUs with details on available license units.</span></span>

``` csharp
// string selectedCustomerId;
// IAggregatePartner partnerOperations;

// To get subscribed SKUs available for group1, the license group for Azure Active Directory (AAD).
List<LicenseGroupId> licenseGroupIds = new List<LicenseGroupId>() { LicenseGroupId.Group1};
var customerUserAadSubscribedSkus = partnerOperations.Customers.ById(selectedCustomerId).SubscribedSkus.Get(licenseGroupIds);

// To get subscribed SKUs available for group2, the license group for Minecraft product licenses.
List<LicenseGroupId> licenseGroupIds = new List<LicenseGroupId>() { LicenseGroupId.Group2};
var customerUserSfbSubscribedSkus = partnerOperations.Customers.ById(selectedCustomerId).SubscribedSkus.Get(licenseGroupIds);

// To get both AAD and Minecraft subscribed SKUs.
List<LicenseGroupId> licenseGroupIds = new List<LicenseGroupId>() { LicenseGroupId.Group1, LicenseGroupId.Group2};
var customerUserBothAadAndSfbSubscribedSkus = partnerOperations.Customers.ById(selectedCustomerId).SubscribedSkus.Get(licenseGroupIds);
```

## <a name="rest-request"></a><span data-ttu-id="01541-122">REST isteği</span><span class="sxs-lookup"><span data-stu-id="01541-122">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="01541-123">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="01541-123">Request syntax</span></span>

| <span data-ttu-id="01541-124">Yöntem</span><span class="sxs-lookup"><span data-stu-id="01541-124">Method</span></span>  | <span data-ttu-id="01541-125">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="01541-125">Request URI</span></span>                                                                                                                                  |
|---------|----------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="01541-126">**Al**</span><span class="sxs-lookup"><span data-stu-id="01541-126">**GET**</span></span> | <span data-ttu-id="01541-127">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-id}/subscribedskus? Licensegroupıds = grup1 http/1.1</span><span class="sxs-lookup"><span data-stu-id="01541-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscribedskus?licenseGroupIds=Group1 HTTP/1.1</span></span>                        |
| <span data-ttu-id="01541-128">**Al**</span><span class="sxs-lookup"><span data-stu-id="01541-128">**GET**</span></span> | <span data-ttu-id="01541-129">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-id}/subscribedskus? Licensegroupıds = grup2 http/1.1</span><span class="sxs-lookup"><span data-stu-id="01541-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscribedskus?licenseGroupIds=Group2 HTTP/1.1</span></span>                        |
| <span data-ttu-id="01541-130">**Al**</span><span class="sxs-lookup"><span data-stu-id="01541-130">**GET**</span></span> | <span data-ttu-id="01541-131">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-id}/subscribedskus? Licensegroupıds = grup1&Licensegroupıds = grup2 http/1.1</span><span class="sxs-lookup"><span data-stu-id="01541-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscribedskus?licenseGroupIds=Group1&licenseGroupIds=Group2 HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="01541-132">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="01541-132">URI parameter</span></span>

<span data-ttu-id="01541-133">Müşteriyi ve lisans gruplarını tanımlamak için aşağıdaki yolu ve sorgu parametrelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="01541-133">Use the following path and query parameters to identify the customer and the license groups.</span></span>

| <span data-ttu-id="01541-134">Ad</span><span class="sxs-lookup"><span data-stu-id="01541-134">Name</span></span>            | <span data-ttu-id="01541-135">Tür</span><span class="sxs-lookup"><span data-stu-id="01541-135">Type</span></span>   | <span data-ttu-id="01541-136">Gerekli</span><span class="sxs-lookup"><span data-stu-id="01541-136">Required</span></span> | <span data-ttu-id="01541-137">Açıklama</span><span class="sxs-lookup"><span data-stu-id="01541-137">Description</span></span>                                                                                                                                                                                                                                                           |
|-----------------|--------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="01541-138">müşteri kimliği</span><span class="sxs-lookup"><span data-stu-id="01541-138">customer-id</span></span>     | <span data-ttu-id="01541-139">string</span><span class="sxs-lookup"><span data-stu-id="01541-139">string</span></span> | <span data-ttu-id="01541-140">Yes</span><span class="sxs-lookup"><span data-stu-id="01541-140">Yes</span></span>      | <span data-ttu-id="01541-141">Müşteriyi tanımlayan GUID biçimli dize.</span><span class="sxs-lookup"><span data-stu-id="01541-141">A GUID formatted string that identifies the customer.</span></span>                                                                                                                                                                                                                 |
| <span data-ttu-id="01541-142">Licensegroupıds</span><span class="sxs-lookup"><span data-stu-id="01541-142">licenseGroupIds</span></span> | <span data-ttu-id="01541-143">dize</span><span class="sxs-lookup"><span data-stu-id="01541-143">string</span></span> | <span data-ttu-id="01541-144">No</span><span class="sxs-lookup"><span data-stu-id="01541-144">No</span></span>       | <span data-ttu-id="01541-145">Atanan lisansların lisans grubunu gösteren bir sabit listesi değeri.</span><span class="sxs-lookup"><span data-stu-id="01541-145">An enum value that indicates the license group of the assigned licenses.</span></span> <span data-ttu-id="01541-146">Geçerli değerler: grup1, grup2 grup1-bu grubun lisansı Azure Active Directory (AAD) içinde yönetilebilecek tüm ürünler vardır.</span><span class="sxs-lookup"><span data-stu-id="01541-146">Valid values: Group1, Group2 Group1 - This group has all products whose license can be managed in the Azure Active Directory (AAD).</span></span> <span data-ttu-id="01541-147">Grup2-bu grup yalnızca Minecrat ürün lisanslarına sahiptir.</span><span class="sxs-lookup"><span data-stu-id="01541-147">Group2 - This group has only Minecraft product licenses.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="01541-148">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="01541-148">Request headers</span></span>

<span data-ttu-id="01541-149">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="01541-149">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="01541-150">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="01541-150">Request body</span></span>

<span data-ttu-id="01541-151">Yok.</span><span class="sxs-lookup"><span data-stu-id="01541-151">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="01541-152">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="01541-152">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/subscribedskus?licenseGroupIds=Group1&licenseGroupIds=Group2 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: a1d077e4-28b1-4578-b873-6d1a82fa1644
MS-CorrelationId: c8cb5a60-ae08-4afc-92f0-efc42adfa186
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="01541-153">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="01541-153">REST response</span></span>

<span data-ttu-id="01541-154">Başarılı olursa, yanıt gövdesi bir [SubscribedSku](license-resources.md#subscribedsku) kaynakları koleksiyonu içerir.</span><span class="sxs-lookup"><span data-stu-id="01541-154">If successful, the response body contains a collection of [SubscribedSku](license-resources.md#subscribedsku) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="01541-155">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="01541-155">Response success and error codes</span></span>

<span data-ttu-id="01541-156">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="01541-156">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="01541-157">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="01541-157">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="01541-158">Tam liste için bkz. [Partner Center hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="01541-158">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="01541-159">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="01541-159">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 4328
Content-Type: application/json; charset=utf-8
MS-CorrelationId: c8cb5a60-ae08-4afc-92f0-efc42adfa186
MS-RequestId: a1d077e4-28b1-4578-b873-6d1a82fa1644
MS-CV: S6Pd5XQAx0Ss/zQi.0
MS-ServerId: 030011719
Date: Sat, 10 Jun 2017 00:19:44 GMT

{
    "totalCount": 04,
    "items": [{
            "availableUnits": 15,
            "activeUnits": 15,
            "consumedUnits": 0,
            "suspendedUnits": 0,
            "totalUnits": 15,
            "warningUnits": 0,
            "productSku": {
                "id": "078d2b04-f1bd-4111-bbd4-b4b1b354cef4",
                "name": "Azure Active Directory Premium P1",
                "skuPartNumber": "AAD_PREMIUM",
                "targetType": "User",
                "licenseGroupId": "group1"
            },
            "servicePlans": [{
                    "displayName": "Exchange Foundation",
                    "serviceName": "EXCHANGE_S_FOUNDATION",
                    "id": "113feb6c-3fe4-4440-bddc-54d774bf0318",
                    "capabilityStatus": "Enabled",
                    "targetType": "Tenant"
                }, {
                    "displayName": "Azure Active Directory Premium P1",
                    "serviceName": "AAD_PREMIUM",
                    "id": "41781fb2-bc02-4b7c-bd55-b576c07bb09d",
                    "capabilityStatus": "Enabled",
                    "targetType": "User"
                }, {
                    "displayName": "Microsoft Azure Multi-Factor Authentication",
                    "serviceName": "MFA_PREMIUM",
                    "id": "8a256a2b-b617-496d-b51b-e76466e88db0",
                    "capabilityStatus": "Enabled",
                    "targetType": "User"
                }
            ],
            "capabilityStatus": "Enabled",
            "attributes": {
                "objectType": "SubscribedSku"
            }
        }, {
            "availableUnits": 1,
            "activeUnits": 1,
            "consumedUnits": 0,
            "suspendedUnits": 0,
            "totalUnits": 1,
            "warningUnits": 0,
            "productSku": {
                "id": "54b84594-9c77-4499-8d65-5e0d5f410e78",
                "name": "Dynamics AX Task",
                "skuPartNumber": "AX_TASK_USER",
                "targetType": "User",
                "licenseGroupId": "group1"
            },
            "servicePlans": [

            ],
            "capabilityStatus": "Enabled",
            "attributes": {
                "objectType": "SubscribedSku"
            }
        }, {
            "availableUnits": 23,
            "activeUnits": 72,
            "consumedUnits": 49,
            "suspendedUnits": 0,
            "totalUnits": 72,
            "warningUnits": 0,
            "productSku": {
                "id": "984df360-9a74-4647-8cf8-696749f6247a",
                "name": "Minecraft Education Edition Faculty",
                "skuPartNumber": "CFQ7TTC0K5DR/0002",
                "targetType": "User",
                "licenseGroupId": "group2"
            },
            "servicePlans": [

            ],
            "capabilityStatus": "Enabled",
            "attributes": {
                "objectType": "SubscribedSku"
            }
        }, {
            "availableUnits": 71,
            "activeUnits": 112,
            "consumedUnits": 41,
            "suspendedUnits": 0,
            "totalUnits": 112,
            "warningUnits": 0,
            "productSku": {
                "id": "1e7e1070-8ccb-4aca-b470-d7cb538cb07e",
                "name": "Windows 10 Enterprise E5",
                "skuPartNumber": "WIN_ENT_E5",
                "targetType": "User",
                "licenseGroupId": "group1"
            },
            "servicePlans": [{
                    "displayName": "Windows Defender Advanced Threat Protection",
                    "serviceName": "WINDEFATP",
                    "id": "871d91ec-ec1a-452b-a83f-bd76c7d770ef",
                    "capabilityStatus": "Enabled",
                    "targetType": "User"
                }, {
                    "displayName": "Windows 10 Enterprise E3",
                    "serviceName": "WIN10_PRO_ENT_SUB",
                    "id": "21b439ba-a0ca-424f-a6cc-52f954a5b111",
                    "capabilityStatus": "Enabled",
                    "targetType": "User"
                }
            ],
            "capabilityStatus": "Enabled",
            "attributes": {
                "objectType": "SubscribedSku"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```

### <a name="response-example-no-matching-skus-found"></a><span data-ttu-id="01541-160">Yanıt örneği (eşleşen SKU bulunamadı)</span><span class="sxs-lookup"><span data-stu-id="01541-160">Response example (no matching SKUs found)</span></span>

<span data-ttu-id="01541-161">Belirtilen lisans grupları için eşleşen bir abone olan SKU bulunamazsa, yanıt, değeri 0 olan totalCount öğesi olan boş bir koleksiyon içerir.</span><span class="sxs-lookup"><span data-stu-id="01541-161">If no matching subscribed SKUs can be found for the specified license groups, the response contains an empty collection with a totalCount element whose value is 0.</span></span>

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
