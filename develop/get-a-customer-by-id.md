---
title: Kimliğe göre müşteri alma
description: Müşteri kimliğine karşılık gelen bir Müşteri kaynağını alır.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: 196d653c789c4b4e1327f0c6e5d2531a18681a71
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/09/2021
ms.locfileid: "111875001"
---
# <a name="get-a-customer-by-id"></a><span data-ttu-id="0b429-103">Kimliğe göre müşteri alma</span><span class="sxs-lookup"><span data-stu-id="0b429-103">Get a customer by ID</span></span>

<span data-ttu-id="0b429-104">**Için geçerlidir:** İş Ortağı Merkezi | İş Ortağı Merkezi 21Vianet | İş Ortağı Merkezi Microsoft Bulut Almanya için | İş Ortağı Merkezi için Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="0b429-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="0b429-105">Müşteri **kimliğine** karşılık gelen bir Müşteri kaynağını alır.</span><span class="sxs-lookup"><span data-stu-id="0b429-105">Gets a **Customer** resource that corresponds to a customer ID.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0b429-106">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="0b429-106">Prerequisites</span></span>

- <span data-ttu-id="0b429-107">kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="0b429-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="0b429-108">Bu senaryo, uygulama+kullanıcı kimlik bilgilerini veya yalnızca uygulama kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="0b429-108">This scenario supports app+user credentials or app-only authentication.</span></span>

- <span data-ttu-id="0b429-109">Müşteri kimliği ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="0b429-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="0b429-110">Müşterinin kimliğini bilmiyorsanız bu kimliği panoda [İş Ortağı Merkezi.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="0b429-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="0b429-111">İş Ortağı Merkezi **menüsünden CSP'yi** ve ardından **Müşteriler'i seçin.**</span><span class="sxs-lookup"><span data-stu-id="0b429-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="0b429-112">Müşteri listesinden müşteriyi ve ardından Hesap'ı **seçin.**</span><span class="sxs-lookup"><span data-stu-id="0b429-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="0b429-113">Müşterinin Hesap sayfasında Müşteri Hesabı Bilgileri **bölümünde Microsoft** **Kimliği'ne** bakın.</span><span class="sxs-lookup"><span data-stu-id="0b429-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="0b429-114">Microsoft Kimliği, müşteri kimliği () ile `customer-tenant-id` aynıdır.</span><span class="sxs-lookup"><span data-stu-id="0b429-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="0b429-115">C\#</span><span class="sxs-lookup"><span data-stu-id="0b429-115">C\#</span></span>

<span data-ttu-id="0b429-116">Kimliğine göre müşteri almak için [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) koleksiyonu kullanın, [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini ve ardından [**Get()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.get) veya [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.getasync) yöntemlerini arayın.</span><span class="sxs-lookup"><span data-stu-id="0b429-116">To get a customer by ID, use your [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) collection, call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method, then call the [**Get()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.getasync) methods.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerIdToRetrieve;

Customer customerInfo = partnerOperations.Customers.ById(customerIdToRetrieve).Get();
```

<span data-ttu-id="0b429-117">**Örnek:** [Konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="0b429-117">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="0b429-118">**Project:** PartnerSDK.FeatureSamples **Sınıfı:** CustomerInformation.cs</span><span class="sxs-lookup"><span data-stu-id="0b429-118">**Project**: PartnerSDK.FeatureSamples **Class**: CustomerInformation.cs</span></span>

## <a name="java"></a><span data-ttu-id="0b429-119">Java</span><span class="sxs-lookup"><span data-stu-id="0b429-119">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="0b429-120">Kimliğine göre müşteri almak için **IAggregatePartner.getCustomers** işlevinizi kullanın, **byId()** işlevini ve **ardından get() işlevini** arayın.</span><span class="sxs-lookup"><span data-stu-id="0b429-120">To get a customer by ID, use your **IAggregatePartner.getCustomers** function, call the **byId()** function, then call the **get()** function.</span></span>

```java
// IAggregatePartner partnerOperations;
// String customerIdToRetrieve;

Customer customerInfo = partnerOperations.getCustomers().byId(customerIdToRetrieve).get();
```

## <a name="powershell"></a><span data-ttu-id="0b429-121">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0b429-121">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="0b429-122">Kimliğine göre müşteri almak için [**Get-PartnerCustomer komutunu**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomer.md) yürütün ve **CustomerId parametresini** belirtin.</span><span class="sxs-lookup"><span data-stu-id="0b429-122">To get a customer by ID, execute the [**Get-PartnerCustomer**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomer.md) command and specify the **CustomerId** parameter.</span></span>

```powershell
Get-PartnerCustomer -CustomerId '2ca7de6c-c05c-46b5-b689-32e53573a97a'
```

## <a name="rest-request"></a><span data-ttu-id="0b429-123">REST isteği</span><span class="sxs-lookup"><span data-stu-id="0b429-123">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="0b429-124">İstek söz dizimi</span><span class="sxs-lookup"><span data-stu-id="0b429-124">Request syntax</span></span>

| <span data-ttu-id="0b429-125">Yöntem</span><span class="sxs-lookup"><span data-stu-id="0b429-125">Method</span></span>  | <span data-ttu-id="0b429-126">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="0b429-126">Request URI</span></span>                                                                            |
|---------|----------------------------------------------------------------------------------------|
| <span data-ttu-id="0b429-127">**Al**</span><span class="sxs-lookup"><span data-stu-id="0b429-127">**GET**</span></span> | <span data-ttu-id="0b429-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="0b429-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="0b429-129">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="0b429-129">URI parameter</span></span>

<span data-ttu-id="0b429-130">Belirli bir müşteriye aşağıdaki sorgu parametresini kullanın.</span><span class="sxs-lookup"><span data-stu-id="0b429-130">Use the following query parameter to a specific customer.</span></span>

| <span data-ttu-id="0b429-131">Ad</span><span class="sxs-lookup"><span data-stu-id="0b429-131">Name</span></span>                   | <span data-ttu-id="0b429-132">Tür</span><span class="sxs-lookup"><span data-stu-id="0b429-132">Type</span></span>     | <span data-ttu-id="0b429-133">Gerekli</span><span class="sxs-lookup"><span data-stu-id="0b429-133">Required</span></span> | <span data-ttu-id="0b429-134">Açıklama</span><span class="sxs-lookup"><span data-stu-id="0b429-134">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="0b429-135">**customer-tenant-id**</span><span class="sxs-lookup"><span data-stu-id="0b429-135">**customer-tenant-id**</span></span> | <span data-ttu-id="0b429-136">**guid**</span><span class="sxs-lookup"><span data-stu-id="0b429-136">**guid**</span></span> | <span data-ttu-id="0b429-137">Y</span><span class="sxs-lookup"><span data-stu-id="0b429-137">Y</span></span>        | <span data-ttu-id="0b429-138">Değer, kurumsal bayinin kurumsal **bayiye** ait olan belirli bir müşteri için sonuçları filtrelemesini sağlayan GUID biçimli bir müşteri kiracı kimliğidir.</span><span class="sxs-lookup"><span data-stu-id="0b429-138">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="0b429-139">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="0b429-139">Request headers</span></span>

<span data-ttu-id="0b429-140">Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="0b429-140">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="0b429-141">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="0b429-141">Request body</span></span>

<span data-ttu-id="0b429-142">Yok.</span><span class="sxs-lookup"><span data-stu-id="0b429-142">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="0b429-143">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="0b429-143">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-CorrelationId: a176c585-b5de-4d65-824c-67a6deb45cd9
MS-RequestId: 74ca1db9-df92-41c6-a362-a16433b0542b
```

## <a name="rest-response"></a><span data-ttu-id="0b429-144">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="0b429-144">REST response</span></span>

<span data-ttu-id="0b429-145">Başarılı olursa, bu yöntem yanıt [gövdesinde](customer-resources.md#customer) bir Müşteri kaynağı döndürür.</span><span class="sxs-lookup"><span data-stu-id="0b429-145">If successful, this method returns a [Customer](customer-resources.md#customer) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="0b429-146">Yanıt başarı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="0b429-146">Response success and error codes</span></span>

<span data-ttu-id="0b429-147">Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="0b429-147">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="0b429-148">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="0b429-148">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="0b429-149">Tam liste için bkz. [Hata Kodları.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="0b429-149">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="0b429-150">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="0b429-150">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1530
Content-Type: application/json; charset=utf-8
MS-CorrelationId: a176c585-b5de-4d65-824c-67a6deb45cd9
MS-RequestId: 74ca1db9-df92-41c6-a362-a16433b0542b

{
  "id": "eebd1b55-5360-4438-a11d-5c06918c3014",
  "commerceId": "99e6a635-48e7-424d-9059-c9db944e3c54",
  "companyProfile": {
    "tenantId": "eebd1b55-5360-4438-a11d-5c06918c3014",
    "domain": "abcdefgh1234.ccsctp.net",
    "companyName": "1kl as kjk",
    "address": {
      "country": "US",
      "region": "wa",
      "city": "redmond",
      "addressLine1": "1 ms way",
      "postalCode": "98052",
      "phoneNumber": "1234567890"
    },
    "email": "a@a.com",
    "links": {
      "self": {
        "uri": "/customers/eebd1b55-5360-4438-a11d-5c06918c3014/profiles/company",
        "method": "GET",
        "headers": []
      }
    },
    "attributes": {
      "objectType": "CustomerCompanyProfile"
    }
  },
  "billingProfile": {
    "id": "eeada110-69d6-4cc9-b093-75feb7ca9d3f",
    "firstName": "d0d89d776d03471c819bf772191ed728",
    "lastName": "kjkAJJAAAAAAAAAAAAAAAAAAAA",
    "email": "a@a.com",
    "culture": "en-US",
    "language": "en",
    "companyName": "1kl as kjkAAAAAAAAAAAAAAAJJJJJJJJJJJAAAAAJJJJJJJJJJJAAJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJAJJJJJAJJAAAAJAJJAAAAAAAAAAAAAAAAAAAA",
    "defaultAddress": {
      "country": "US",
      "city": "redmond",
      "state": "WA",
      "addressLine1": "1 ms way",
      "postalCode": "98052",
      "firstName": "1kl as",
      "lastName": "kjk",
      "phoneNumber": "1234567890"
    },
    "links": {
      "self": {
        "uri": "/customers/eebd1b55-5360-4438-a11d-5c06918c3014/profiles/billing",
        "method": "GET",
        "headers": [

        ]
      }
    },
    "attributes": {
      "etag": "-4242348048554929329",
      "objectType": "CustomerBillingProfile"
    }
  },
  "relationshipToPartner": "reseller",
  "allowDelegatedAccess": true,
  "customDomains": [
    "abcdefgh1234.ccsctp.net"
  ],
  "links": {
    "self": {
      "uri": "/customers/eebd1b55-5360-4438-a11d-5c06918c3014",
      "method": "GET",
      "headers": []
    }
  },
  "attributes": {
    "objectType": "Customer"
  }
}
```
