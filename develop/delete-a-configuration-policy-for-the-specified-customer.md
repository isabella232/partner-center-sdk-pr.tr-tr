---
title: Belirtilen müşteri için yeni bir yapılandırma ilkesini silme
description: Belirtilen müşteri ve ilke tanımlayıcısı için yapılandırma ilkesini silme.
ms.date: 06/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 586878367fc0873ef0fb1415799b2b7022954053
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/22/2020
ms.locfileid: "97769389"
---
# <a name="delete-a-configuration-policy-for-the-specified-customer"></a><span data-ttu-id="5d5d5-103">Belirtilen müşteri için yeni bir yapılandırma ilkesini silme</span><span class="sxs-lookup"><span data-stu-id="5d5d5-103">Delete a configuration policy for the specified customer</span></span>

<span data-ttu-id="5d5d5-104">**Uygulama hedefi:**</span><span class="sxs-lookup"><span data-stu-id="5d5d5-104">**Applies to:**</span></span>

- <span data-ttu-id="5d5d5-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="5d5d5-105">Partner Center</span></span>
- <span data-ttu-id="5d5d5-106">Microsoft Bulut Almanya için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="5d5d5-106">Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="5d5d5-107">Belirtilen müşteri ve ilke tanımlayıcısı için yapılandırma ilkesini silme.</span><span class="sxs-lookup"><span data-stu-id="5d5d5-107">How to delete a configuration policy for a specified customer and policy identifier.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5d5d5-108">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="5d5d5-108">Prerequisites</span></span>

- <span data-ttu-id="5d5d5-109">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="5d5d5-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="5d5d5-110">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="5d5d5-110">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="5d5d5-111">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="5d5d5-111">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="5d5d5-112">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5d5d5-112">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="5d5d5-113">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="5d5d5-113">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="5d5d5-114">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="5d5d5-114">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="5d5d5-115">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="5d5d5-115">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="5d5d5-116">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="5d5d5-116">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="5d5d5-117">İlke tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="5d5d5-117">The policy identifier.</span></span>

## <a name="c"></a><span data-ttu-id="5d5d5-118">C\#</span><span class="sxs-lookup"><span data-stu-id="5d5d5-118">C\#</span></span>

<span data-ttu-id="5d5d5-119">Belirtilen bir müşterinin yapılandırma ilkesini silmek için:</span><span class="sxs-lookup"><span data-stu-id="5d5d5-119">To delete a configuration policy for a specified customer:</span></span>

1. <span data-ttu-id="5d5d5-120">Belirtilen müşterideki işlemlere bir arabirim almak için, müşteri KIMLIĞIYLE [**ıaggregatepartner. Customers. Byıd**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="5d5d5-120">Call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to retrieve an interface to operations on the specified customer.</span></span>

2. <span data-ttu-id="5d5d5-121">Belirtilen ilke için yapılandırma ilkesi işlemlerine bir arabirim almak üzere ilke KIMLIĞIYLE [**Configurationpolicies. Byıd**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.byid) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="5d5d5-121">Call the [**ConfigurationPolicies.ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.byid) method with the policy ID to retrieve an interface to configuration policy operations for the specified policy.</span></span>

3. <span data-ttu-id="5d5d5-122">Yapılandırma ilkesini silmek için [**Delete**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.delete) veya [**DeleteAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.deleteasync) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="5d5d5-122">Call the [**Delete**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.delete) or [**DeleteAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.deleteasync) method to delete the configuration policy.</span></span>

``` csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;
string selectedPolicyId;

partnerOperations.Customers.ById(selectedCustomerId).ConfigurationPolicies.ById(selectedPolicyId).Delete();
```

<span data-ttu-id="5d5d5-123">**Örnek**: [konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="5d5d5-123">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="5d5d5-124">**Proje**: Iş Ortağı Merkezi SDK örnekleri **sınıfı**: DeleteConfigurationPolicy.cs</span><span class="sxs-lookup"><span data-stu-id="5d5d5-124">**Project**: Partner Center SDK Samples **Class**: DeleteConfigurationPolicy.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="5d5d5-125">REST isteği</span><span class="sxs-lookup"><span data-stu-id="5d5d5-125">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="5d5d5-126">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="5d5d5-126">Request syntax</span></span>

| <span data-ttu-id="5d5d5-127">Yöntem</span><span class="sxs-lookup"><span data-stu-id="5d5d5-127">Method</span></span>     | <span data-ttu-id="5d5d5-128">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="5d5d5-128">Request URI</span></span>                                                                                          |
|------------|------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="5d5d5-129">**SILMELI**</span><span class="sxs-lookup"><span data-stu-id="5d5d5-129">**DELETE**</span></span> | <span data-ttu-id="5d5d5-130">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-id}/policies/{Policy-ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="5d5d5-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/policies/{policy-id} HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="5d5d5-131">URI parametreleri</span><span class="sxs-lookup"><span data-stu-id="5d5d5-131">URI parameters</span></span>

<span data-ttu-id="5d5d5-132">İsteği oluştururken aşağıdaki yol parametrelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="5d5d5-132">Use the following path parameters when creating the request.</span></span>

| <span data-ttu-id="5d5d5-133">Ad</span><span class="sxs-lookup"><span data-stu-id="5d5d5-133">Name</span></span>        | <span data-ttu-id="5d5d5-134">Tür</span><span class="sxs-lookup"><span data-stu-id="5d5d5-134">Type</span></span>   | <span data-ttu-id="5d5d5-135">Gerekli</span><span class="sxs-lookup"><span data-stu-id="5d5d5-135">Required</span></span> | <span data-ttu-id="5d5d5-136">Açıklama</span><span class="sxs-lookup"><span data-stu-id="5d5d5-136">Description</span></span>                                                   |
|-------------|--------|----------|---------------------------------------------------------------|
| <span data-ttu-id="5d5d5-137">müşteri kimliği</span><span class="sxs-lookup"><span data-stu-id="5d5d5-137">customer-id</span></span> | <span data-ttu-id="5d5d5-138">string</span><span class="sxs-lookup"><span data-stu-id="5d5d5-138">string</span></span> | <span data-ttu-id="5d5d5-139">Yes</span><span class="sxs-lookup"><span data-stu-id="5d5d5-139">Yes</span></span>      | <span data-ttu-id="5d5d5-140">Müşteriyi tanımlayan GUID biçimli bir dize.</span><span class="sxs-lookup"><span data-stu-id="5d5d5-140">A GUID-formatted string that identifies the customer.</span></span>         |
| <span data-ttu-id="5d5d5-141">ilke kimliği</span><span class="sxs-lookup"><span data-stu-id="5d5d5-141">policy-id</span></span>   | <span data-ttu-id="5d5d5-142">string</span><span class="sxs-lookup"><span data-stu-id="5d5d5-142">string</span></span> | <span data-ttu-id="5d5d5-143">Yes</span><span class="sxs-lookup"><span data-stu-id="5d5d5-143">Yes</span></span>      | <span data-ttu-id="5d5d5-144">Silinecek ilkeyi tanımlayan GUID biçimli bir dize.</span><span class="sxs-lookup"><span data-stu-id="5d5d5-144">A GUID-formatted string that identifies the policy to delete.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="5d5d5-145">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="5d5d5-145">Request headers</span></span>

<span data-ttu-id="5d5d5-146">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="5d5d5-146">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="5d5d5-147">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="5d5d5-147">Request body</span></span>

<span data-ttu-id="5d5d5-148">Yok</span><span class="sxs-lookup"><span data-stu-id="5d5d5-148">None</span></span>

### <a name="request-example"></a><span data-ttu-id="5d5d5-149">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="5d5d5-149">Request example</span></span>

```http
DELETE https://api.partnercenter.microsoft.com/v1/customers/47021739-3426-40bf-9601-61b4b6d7c793/policies/56edf752-ee77-4fd8-b7f5-df1f74a3a9ac HTTP/1.1
Authorization: Bearer <token>
MS-RequestId: e88d014d-ab70-41de-90a0-f7fd1797267d
MS-CorrelationId: de894e18-f027-4ac0-8b5a-34f0c222af0c
X-Locale: en-US
Content-Length: 0
Content-Type: application/json
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="5d5d5-150">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="5d5d5-150">REST response</span></span>

<span data-ttu-id="5d5d5-151">Başarılı olursa, yanıt 204 Içerik durum kodu döndürür.</span><span class="sxs-lookup"><span data-stu-id="5d5d5-151">If successful, the response returns a 204 No Content status code.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="5d5d5-152">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="5d5d5-152">Response success and error codes</span></span>

<span data-ttu-id="5d5d5-153">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="5d5d5-153">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="5d5d5-154">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="5d5d5-154">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="5d5d5-155">Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="5d5d5-155">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="5d5d5-156">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="5d5d5-156">Response example</span></span>

```http
HTTP/1.1 204 No Content
Content-Length: 0
MS-CorrelationId: cee5caf4-c322-4baa-b1d7-e94afb9891a4
MS-RequestId: 76b6f317-1da1-4b61-a6fd-9952439a2c46
MS-CV: YrLe3w6BbUSMt1fi.0
MS-ServerId: 030020344
Date: Tue, 25 Jul 2017 18:10:41 GMT
```
