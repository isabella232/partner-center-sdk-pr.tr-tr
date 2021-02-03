---
title: Kimliğe göre müşteri alma
description: Müşteri KIMLIĞINE karşılık gelen bir müşteri kaynağını alır.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: dd4301dbb6f749b675fe624daf7f63751806f856
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/22/2020
ms.locfileid: "97769377"
---
# <a name="get-a-customer-by-id"></a><span data-ttu-id="ff10c-103">Kimliğe göre müşteri alma</span><span class="sxs-lookup"><span data-stu-id="ff10c-103">Get a customer by ID</span></span>

<span data-ttu-id="ff10c-104">**Uygulama hedefi**</span><span class="sxs-lookup"><span data-stu-id="ff10c-104">**Applies To**</span></span>

- <span data-ttu-id="ff10c-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="ff10c-105">Partner Center</span></span>
- <span data-ttu-id="ff10c-106">21Vianet tarafından çalıştırılan iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="ff10c-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="ff10c-107">Microsoft Bulut Almanya için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="ff10c-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="ff10c-108">Microsoft Cloud for US Government için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="ff10c-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="ff10c-109">Müşteri KIMLIĞINE karşılık gelen bir **Müşteri** kaynağını alır.</span><span class="sxs-lookup"><span data-stu-id="ff10c-109">Gets a **Customer** resource that corresponds to a customer ID.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ff10c-110">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="ff10c-110">Prerequisites</span></span>

- <span data-ttu-id="ff10c-111">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="ff10c-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="ff10c-112">Bu senaryo, uygulama + kullanıcı kimlik bilgilerini veya yalnızca uygulama kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="ff10c-112">This scenario supports app+user credentials or app-only authentication.</span></span>

- <span data-ttu-id="ff10c-113">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="ff10c-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="ff10c-114">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ff10c-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="ff10c-115">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="ff10c-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="ff10c-116">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="ff10c-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="ff10c-117">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="ff10c-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="ff10c-118">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="ff10c-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="ff10c-119">C\#</span><span class="sxs-lookup"><span data-stu-id="ff10c-119">C\#</span></span>

<span data-ttu-id="ff10c-120">Bir müşteriyi KIMLIĞE göre almak için [**ıaggregatepartner. Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) koleksiyonunuzu kullanın, [**byıd ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini çağırın, sonra [**Get ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.get) veya [**GetAsync ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.getasync) yöntemlerini çağırın.</span><span class="sxs-lookup"><span data-stu-id="ff10c-120">To get a customer by ID, use your [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) collection, call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method, then call the [**Get()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.getasync) methods.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerIdToRetrieve;

Customer customerInfo = partnerOperations.Customers.ById(customerIdToRetrieve).Get();
```

<span data-ttu-id="ff10c-121">**Örnek**: [konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="ff10c-121">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="ff10c-122">**Proje**: partnersdk. Featuresamples **sınıfı**: CustomerInformation.cs</span><span class="sxs-lookup"><span data-stu-id="ff10c-122">**Project**: PartnerSDK.FeatureSamples **Class**: CustomerInformation.cs</span></span>

## <a name="java"></a><span data-ttu-id="ff10c-123">Java</span><span class="sxs-lookup"><span data-stu-id="ff10c-123">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="ff10c-124">Bir müşteriyi KIMLIĞE göre almak için **ıaggregatepartner. getCustomers** işlevini kullanın, **byıd ()** işlevini çağırın ve sonra **Get ()** işlevini çağırın.</span><span class="sxs-lookup"><span data-stu-id="ff10c-124">To get a customer by ID, use your **IAggregatePartner.getCustomers** function, call the **byId()** function, then call the **get()** function.</span></span>

```java
// IAggregatePartner partnerOperations;
// String customerIdToRetrieve;

Customer customerInfo = partnerOperations.getCustomers().byId(customerIdToRetrieve).get();
```

## <a name="powershell"></a><span data-ttu-id="ff10c-125">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ff10c-125">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="ff10c-126">Müşteriyi KIMLIĞE göre almak için, [**Get-PartnerCustomer**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomer.md) komutunu yürütün ve **CustomerID** parametresini belirtin.</span><span class="sxs-lookup"><span data-stu-id="ff10c-126">To get a customer by ID, execute the [**Get-PartnerCustomer**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomer.md) command and specify the **CustomerId** parameter.</span></span>

```powershell
Get-PartnerCustomer -CustomerId '2ca7de6c-c05c-46b5-b689-32e53573a97a'
```

## <a name="rest-request"></a><span data-ttu-id="ff10c-127">REST isteği</span><span class="sxs-lookup"><span data-stu-id="ff10c-127">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="ff10c-128">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="ff10c-128">Request syntax</span></span>

| <span data-ttu-id="ff10c-129">Yöntem</span><span class="sxs-lookup"><span data-stu-id="ff10c-129">Method</span></span>  | <span data-ttu-id="ff10c-130">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="ff10c-130">Request URI</span></span>                                                                            |
|---------|----------------------------------------------------------------------------------------|
| <span data-ttu-id="ff10c-131">**Al**</span><span class="sxs-lookup"><span data-stu-id="ff10c-131">**GET**</span></span> | <span data-ttu-id="ff10c-132">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="ff10c-132">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="ff10c-133">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="ff10c-133">URI parameter</span></span>

<span data-ttu-id="ff10c-134">Belirli bir müşteri için aşağıdaki sorgu parametresini kullanın.</span><span class="sxs-lookup"><span data-stu-id="ff10c-134">Use the following query parameter to a specific customer.</span></span>

| <span data-ttu-id="ff10c-135">Ad</span><span class="sxs-lookup"><span data-stu-id="ff10c-135">Name</span></span>                   | <span data-ttu-id="ff10c-136">Tür</span><span class="sxs-lookup"><span data-stu-id="ff10c-136">Type</span></span>     | <span data-ttu-id="ff10c-137">Gerekli</span><span class="sxs-lookup"><span data-stu-id="ff10c-137">Required</span></span> | <span data-ttu-id="ff10c-138">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ff10c-138">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="ff10c-139">**Müşteri-Kiracı kimliği**</span><span class="sxs-lookup"><span data-stu-id="ff10c-139">**customer-tenant-id**</span></span> | <span data-ttu-id="ff10c-140">**guid**</span><span class="sxs-lookup"><span data-stu-id="ff10c-140">**guid**</span></span> | <span data-ttu-id="ff10c-141">Y</span><span class="sxs-lookup"><span data-stu-id="ff10c-141">Y</span></span>        | <span data-ttu-id="ff10c-142">Değer, satıcının satıcıya ait olan belirli bir müşteriye ait sonuçları filtrelemesine olanak tanıyan bir GUID biçimli **Müşteri-Kiracı kimliği** ' dir.</span><span class="sxs-lookup"><span data-stu-id="ff10c-142">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="ff10c-143">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="ff10c-143">Request headers</span></span>

<span data-ttu-id="ff10c-144">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="ff10c-144">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="ff10c-145">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="ff10c-145">Request body</span></span>

<span data-ttu-id="ff10c-146">Yok.</span><span class="sxs-lookup"><span data-stu-id="ff10c-146">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="ff10c-147">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="ff10c-147">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-CorrelationId: a176c585-b5de-4d65-824c-67a6deb45cd9
MS-RequestId: 74ca1db9-df92-41c6-a362-a16433b0542b
```

## <a name="rest-response"></a><span data-ttu-id="ff10c-148">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="ff10c-148">REST response</span></span>

<span data-ttu-id="ff10c-149">Başarılı olursa, bu yöntem yanıt gövdesinde bir [Müşteri](customer-resources.md#customer) kaynağı döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff10c-149">If successful, this method returns a [Customer](customer-resources.md#customer) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="ff10c-150">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="ff10c-150">Response success and error codes</span></span>

<span data-ttu-id="ff10c-151">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="ff10c-151">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="ff10c-152">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="ff10c-152">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="ff10c-153">Tam liste için bkz. [hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="ff10c-153">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="ff10c-154">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="ff10c-154">Response example</span></span>

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
