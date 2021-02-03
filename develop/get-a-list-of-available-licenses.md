---
title: Kullanılabilir lisansların bir listesini alma
description: Belirtilen müşterinin kullanıcılarına sunulan lisansların listesini alma.
ms.date: 07/25/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: f675e5b96b2f2040d662c0dc7f1e06625f267689
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769545"
---
# <a name="get-a-list-of-available-licenses"></a><span data-ttu-id="07433-103">Kullanılabilir lisansların bir listesini alma</span><span class="sxs-lookup"><span data-stu-id="07433-103">Get a list of available licenses</span></span>

<span data-ttu-id="07433-104">**Uygulama hedefi:**</span><span class="sxs-lookup"><span data-stu-id="07433-104">**Applies to:**</span></span>

- <span data-ttu-id="07433-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="07433-105">Partner Center</span></span>

<span data-ttu-id="07433-106">Bu makalede, belirtilen müşterinin kullanıcılarına sunulan lisansların bir listesini alma açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="07433-106">This article describes how to get a list of licenses available to users of the specified customer.</span></span>

<span data-ttu-id="07433-107">Aşağıdaki örnekler, Azure Active Directory (Azure AD) tarafından yönetilen lisansları temsil eden varsayılan lisans grubu olan **grup1**'ten kullanılabilen lisansları geri döndürür.</span><span class="sxs-lookup"><span data-stu-id="07433-107">The following examples return licenses available from **group1**, the default license group that represents licenses managed by Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="07433-108">Belirtilen bir lisans grubuna yönelik kullanılabilir lisanslar almak için, bkz. [lisans grubuna göre kullanılabilir lisansların listesini al](get-a-list-of-available-licenses-by-license-group.md).</span><span class="sxs-lookup"><span data-stu-id="07433-108">To get available licenses for a specified license group, see [Get a list of available licenses by license group](get-a-list-of-available-licenses-by-license-group.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="07433-109">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="07433-109">Prerequisites</span></span>

- <span data-ttu-id="07433-110">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="07433-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="07433-111">Bu senaryo yalnızca uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="07433-111">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="07433-112">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="07433-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="07433-113">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="07433-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="07433-114">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="07433-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="07433-115">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="07433-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="07433-116">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="07433-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="07433-117">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="07433-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="07433-118">C\#</span><span class="sxs-lookup"><span data-stu-id="07433-118">C\#</span></span>

<span data-ttu-id="07433-119">Varsayılan lisans grubundan bir müşterinin kullanıcılarına sunulan lisansların listesini almak için:</span><span class="sxs-lookup"><span data-stu-id="07433-119">To retrieve the list of licenses available from the default license group to users of a customer:</span></span>

1. <span data-ttu-id="07433-120">Müşteriyi tanımlamak için, müşteri KIMLIĞIYLE [**ıaggregatepartner. Customers. Byıd**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini kullanın.</span><span class="sxs-lookup"><span data-stu-id="07433-120">Use the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span>

2. <span data-ttu-id="07433-121">Müşteri abone olunan SKU toplama işlemlerine bir arabirim almak için [**SubscribedSkus**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscribedskus) özelliğinin değerini alın.</span><span class="sxs-lookup"><span data-stu-id="07433-121">Get the value of the [**SubscribedSkus**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscribedskus) property to retrieve an interface to customer subscribed SKU collection operations.</span></span>

3. <span data-ttu-id="07433-122">Lisans listesini almak için [**Get**](/dotnet/api/microsoft.store.partnercenter.subscribedskus.icustomersubscribedskucollection.get) veya [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscribedskus.icustomersubscribedskucollection.getasync) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="07433-122">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.subscribedskus.icustomersubscribedskucollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscribedskus.icustomersubscribedskucollection.getasync) method to retrieve the list of licenses.</span></span>

``` csharp
// string selectedCustomerId;
// IAggregatePartner partnerOperations;

var customerUserSubscribedSkus = partnerOperations.Customers.ById(selectedCustomerId).SubscribedSkus.Get();
```

<span data-ttu-id="07433-123">Bir örnek için aşağıdakilere bakın:</span><span class="sxs-lookup"><span data-stu-id="07433-123">For an example, see the following:</span></span>

- <span data-ttu-id="07433-124">Örnek: [konsol test uygulaması](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="07433-124">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="07433-125">Proje: **Iş ortağı MERKEZI SDK örnekleri**</span><span class="sxs-lookup"><span data-stu-id="07433-125">Project: **Partner Center SDK Samples**</span></span>
- <span data-ttu-id="07433-126">Sınıf: **GetCustomerSubscribedSkus.cs**</span><span class="sxs-lookup"><span data-stu-id="07433-126">Class: **GetCustomerSubscribedSkus.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="07433-127">REST isteği</span><span class="sxs-lookup"><span data-stu-id="07433-127">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="07433-128">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="07433-128">Request syntax</span></span>

| <span data-ttu-id="07433-129">Yöntem</span><span class="sxs-lookup"><span data-stu-id="07433-129">Method</span></span>  | <span data-ttu-id="07433-130">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="07433-130">Request URI</span></span>                                                                                    |
|---------|------------------------------------------------------------------------------------------------|
| <span data-ttu-id="07433-131">**Al**</span><span class="sxs-lookup"><span data-stu-id="07433-131">**GET**</span></span> | <span data-ttu-id="07433-132">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-id}/subscribedskus http/1.1</span><span class="sxs-lookup"><span data-stu-id="07433-132">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscribedskus HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="07433-133">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="07433-133">URI parameter</span></span>

<span data-ttu-id="07433-134">Müşteriyi tanımlamak için aşağıdaki yol parametresini kullanın.</span><span class="sxs-lookup"><span data-stu-id="07433-134">Use the following path parameter to identify the customer.</span></span>

| <span data-ttu-id="07433-135">Ad</span><span class="sxs-lookup"><span data-stu-id="07433-135">Name</span></span>        | <span data-ttu-id="07433-136">Tür</span><span class="sxs-lookup"><span data-stu-id="07433-136">Type</span></span>   | <span data-ttu-id="07433-137">Gerekli</span><span class="sxs-lookup"><span data-stu-id="07433-137">Required</span></span> | <span data-ttu-id="07433-138">Açıklama</span><span class="sxs-lookup"><span data-stu-id="07433-138">Description</span></span>                                           |
|-------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="07433-139">müşteri kimliği</span><span class="sxs-lookup"><span data-stu-id="07433-139">customer-id</span></span> | <span data-ttu-id="07433-140">string</span><span class="sxs-lookup"><span data-stu-id="07433-140">string</span></span> | <span data-ttu-id="07433-141">Yes</span><span class="sxs-lookup"><span data-stu-id="07433-141">Yes</span></span>      | <span data-ttu-id="07433-142">Müşteriyi tanımlayan GUID biçimli dize.</span><span class="sxs-lookup"><span data-stu-id="07433-142">A GUID formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="07433-143">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="07433-143">Request headers</span></span>

<span data-ttu-id="07433-144">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="07433-144">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="07433-145">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="07433-145">Request body</span></span>

<span data-ttu-id="07433-146">Yok.</span><span class="sxs-lookup"><span data-stu-id="07433-146">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="07433-147">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="07433-147">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/subscribedskus HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 53308f82-1bf7-44e2-8dda-4517e4688bd4
MS-CorrelationId: 95660db2-7425-4021-babe-a26ddbcb0187
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="07433-148">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="07433-148">REST response</span></span>

<span data-ttu-id="07433-149">Başarılı olursa, yanıt gövdesi bir [SubscribedSku](license-resources.md#subscribedsku) kaynakları koleksiyonu içerir.</span><span class="sxs-lookup"><span data-stu-id="07433-149">If successful, the response body contains a collection of [SubscribedSku](license-resources.md#subscribedsku) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="07433-150">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="07433-150">Response success and error codes</span></span>

<span data-ttu-id="07433-151">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="07433-151">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="07433-152">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="07433-152">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="07433-153">Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="07433-153">For a full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="07433-154">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="07433-154">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 4859
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 95660db2-7425-4021-babe-a26ddbcb0187
MS-RequestId: 53308f82-1bf7-44e2-8dda-4517e4688bd4
MS-CV: 7BQ0jitzXUCLwRM6.0
MS-ServerId: 020021921
Date: Fri, 09 Jun 2017 17:50:46 GMT

 {
    "totalCount": 2,
    "items": [{
            "availableUnits": 4,
            "activeUnits": 5,
            "consumedUnits": 1,
            "suspendedUnits": 0,
            "totalUnits": 5,
            "warningUnits": 0,
            "productSku": {
                "id": "efccb6f7-5641-4e0e-bd10-b4976e1bf68e",
                "name": "Enterprise Mobility + Security E3",
                "skuPartNumber": "EMS",
                "targetType": "User",
                "licenseGroupId": "group1"
            },
            "servicePlans": [{
                    "displayName": "Azure Information Protection Premium P1",
                    "serviceName": "RMS_S_PREMIUM",
                    "id": "6c57d4b6-3b23-47a5-9bc9-69f17b4947b3",
                    "capabilityStatus": "Enabled",
                    "targetType": "User"
                }, {
                    "displayName": "Microsoft Intune A Direct",
                    "serviceName": "INTUNE_A",
                    "id": "c1ec4a95-1f05-45b3-a911-aa3fa01094f5",
                    "capabilityStatus": "Enabled",
                    "targetType": "User"
                }, {
                    "displayName": "Microsoft Azure Active Directory Rights",
                    "serviceName": "RMS_S_ENTERPRISE",
                    "id": "bea4c11e-220a-4e6d-8eb8-8ea15d019f90",
                    "capabilityStatus": "Enabled",
                    "targetType": "User"
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
        },  {
            "availableUnits": 0,
            "activeUnits": 1,
            "consumedUnits": 1,
            "suspendedUnits": 0,
            "totalUnits": 1,
            "warningUnits": 0,
            "productSku": {
                "id": "f8a1db68-be16-40ed-86d5-cb42ce701560",
                "name": "Power BI Pro",
                "skuPartNumber": "POWER_BI_PRO",
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
                    "displayName": "Power BI Pro",
                    "serviceName": "BI_AZURE_P2",
                    "id": "70d33638-9c74-4d01-bfd3-562de28bd4ba",
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
