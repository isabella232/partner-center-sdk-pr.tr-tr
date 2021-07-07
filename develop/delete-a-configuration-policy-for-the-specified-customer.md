---
title: Belirtilen müşteri için yeni bir yapılandırma ilkesini silme
description: Belirtilen müşteri ve ilke tanımlayıcısı için yapılandırma ilkesini silme.
ms.date: 06/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 2d6a7d392bd6af6850eb7716528e6745943bb7bb
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973035"
---
# <a name="delete-a-configuration-policy-for-the-specified-customer"></a><span data-ttu-id="43b9c-103">Belirtilen müşteri için yeni bir yapılandırma ilkesini silme</span><span class="sxs-lookup"><span data-stu-id="43b9c-103">Delete a configuration policy for the specified customer</span></span>

<span data-ttu-id="43b9c-104">**Uygulama hedefi**: Iş Ortağı Merkezi | Microsoft Bulut Almanya için iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="43b9c-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="43b9c-105">Belirtilen müşteri ve ilke tanımlayıcısı için yapılandırma ilkesini silme.</span><span class="sxs-lookup"><span data-stu-id="43b9c-105">How to delete a configuration policy for a specified customer and policy identifier.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="43b9c-106">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="43b9c-106">Prerequisites</span></span>

- <span data-ttu-id="43b9c-107">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="43b9c-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="43b9c-108">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="43b9c-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="43b9c-109">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="43b9c-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="43b9c-110">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="43b9c-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="43b9c-111">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="43b9c-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="43b9c-112">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="43b9c-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="43b9c-113">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="43b9c-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="43b9c-114">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="43b9c-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="43b9c-115">İlke tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="43b9c-115">The policy identifier.</span></span>

## <a name="c"></a><span data-ttu-id="43b9c-116">C\#</span><span class="sxs-lookup"><span data-stu-id="43b9c-116">C\#</span></span>

<span data-ttu-id="43b9c-117">Belirtilen bir müşterinin yapılandırma ilkesini silmek için:</span><span class="sxs-lookup"><span data-stu-id="43b9c-117">To delete a configuration policy for a specified customer:</span></span>

1. <span data-ttu-id="43b9c-118">Belirtilen müşterideki işlemlere bir arabirim almak için, müşteri KIMLIĞIYLE [**ıaggregatepartner. Customers. Byıd**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="43b9c-118">Call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to retrieve an interface to operations on the specified customer.</span></span>

2. <span data-ttu-id="43b9c-119">Belirtilen ilke için yapılandırma ilkesi işlemlerine bir arabirim almak üzere ilke KIMLIĞIYLE [**Configurationpolicies. Byıd**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.byid) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="43b9c-119">Call the [**ConfigurationPolicies.ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.byid) method with the policy ID to retrieve an interface to configuration policy operations for the specified policy.</span></span>

3. <span data-ttu-id="43b9c-120">Yapılandırma ilkesini silmek için [**Delete**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.delete) veya [**DeleteAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.deleteasync) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="43b9c-120">Call the [**Delete**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.delete) or [**DeleteAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.deleteasync) method to delete the configuration policy.</span></span>

``` csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;
string selectedPolicyId;

partnerOperations.Customers.ById(selectedCustomerId).ConfigurationPolicies.ById(selectedPolicyId).Delete();
```

<span data-ttu-id="43b9c-121">**Örnek**: [konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="43b9c-121">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="43b9c-122">**Project**: iş ortağı merkezi SDK örnekleri **sınıfı**: deleteconfigurationpolicy. cs</span><span class="sxs-lookup"><span data-stu-id="43b9c-122">**Project**: Partner Center SDK Samples **Class**: DeleteConfigurationPolicy.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="43b9c-123">REST isteği</span><span class="sxs-lookup"><span data-stu-id="43b9c-123">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="43b9c-124">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="43b9c-124">Request syntax</span></span>

| <span data-ttu-id="43b9c-125">Yöntem</span><span class="sxs-lookup"><span data-stu-id="43b9c-125">Method</span></span>     | <span data-ttu-id="43b9c-126">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="43b9c-126">Request URI</span></span>                                                                                          |
|------------|------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="43b9c-127">**SILMELI**</span><span class="sxs-lookup"><span data-stu-id="43b9c-127">**DELETE**</span></span> | <span data-ttu-id="43b9c-128">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-id}/policies/{Policy-ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="43b9c-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/policies/{policy-id} HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="43b9c-129">URI parametreleri</span><span class="sxs-lookup"><span data-stu-id="43b9c-129">URI parameters</span></span>

<span data-ttu-id="43b9c-130">İsteği oluştururken aşağıdaki yol parametrelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="43b9c-130">Use the following path parameters when creating the request.</span></span>

| <span data-ttu-id="43b9c-131">Ad</span><span class="sxs-lookup"><span data-stu-id="43b9c-131">Name</span></span>        | <span data-ttu-id="43b9c-132">Tür</span><span class="sxs-lookup"><span data-stu-id="43b9c-132">Type</span></span>   | <span data-ttu-id="43b9c-133">Gerekli</span><span class="sxs-lookup"><span data-stu-id="43b9c-133">Required</span></span> | <span data-ttu-id="43b9c-134">Açıklama</span><span class="sxs-lookup"><span data-stu-id="43b9c-134">Description</span></span>                                                   |
|-------------|--------|----------|---------------------------------------------------------------|
| <span data-ttu-id="43b9c-135">müşteri kimliği</span><span class="sxs-lookup"><span data-stu-id="43b9c-135">customer-id</span></span> | <span data-ttu-id="43b9c-136">string</span><span class="sxs-lookup"><span data-stu-id="43b9c-136">string</span></span> | <span data-ttu-id="43b9c-137">Yes</span><span class="sxs-lookup"><span data-stu-id="43b9c-137">Yes</span></span>      | <span data-ttu-id="43b9c-138">Müşteriyi tanımlayan GUID biçimli bir dize.</span><span class="sxs-lookup"><span data-stu-id="43b9c-138">A GUID-formatted string that identifies the customer.</span></span>         |
| <span data-ttu-id="43b9c-139">ilke kimliği</span><span class="sxs-lookup"><span data-stu-id="43b9c-139">policy-id</span></span>   | <span data-ttu-id="43b9c-140">string</span><span class="sxs-lookup"><span data-stu-id="43b9c-140">string</span></span> | <span data-ttu-id="43b9c-141">Yes</span><span class="sxs-lookup"><span data-stu-id="43b9c-141">Yes</span></span>      | <span data-ttu-id="43b9c-142">Silinecek ilkeyi tanımlayan GUID biçimli bir dize.</span><span class="sxs-lookup"><span data-stu-id="43b9c-142">A GUID-formatted string that identifies the policy to delete.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="43b9c-143">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="43b9c-143">Request headers</span></span>

<span data-ttu-id="43b9c-144">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="43b9c-144">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="43b9c-145">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="43b9c-145">Request body</span></span>

<span data-ttu-id="43b9c-146">Hiçbiri</span><span class="sxs-lookup"><span data-stu-id="43b9c-146">None</span></span>

### <a name="request-example"></a><span data-ttu-id="43b9c-147">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="43b9c-147">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="43b9c-148">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="43b9c-148">REST response</span></span>

<span data-ttu-id="43b9c-149">Başarılı olursa, yanıt 204 Içerik durum kodu döndürür.</span><span class="sxs-lookup"><span data-stu-id="43b9c-149">If successful, the response returns a 204 No Content status code.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="43b9c-150">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="43b9c-150">Response success and error codes</span></span>

<span data-ttu-id="43b9c-151">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="43b9c-151">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="43b9c-152">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="43b9c-152">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="43b9c-153">Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="43b9c-153">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="43b9c-154">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="43b9c-154">Response example</span></span>

```http
HTTP/1.1 204 No Content
Content-Length: 0
MS-CorrelationId: cee5caf4-c322-4baa-b1d7-e94afb9891a4
MS-RequestId: 76b6f317-1da1-4b61-a6fd-9952439a2c46
MS-CV: YrLe3w6BbUSMt1fi.0
MS-ServerId: 030020344
Date: Tue, 25 Jul 2017 18:10:41 GMT
```
