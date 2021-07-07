---
title: Deneme aboneliğini ücretli aboneliğe dönüştürme
description: Deneme aboneliğini ücretli İş Ortağı Merkezi api'leri kullanmayı öğrenin.
ms.date: 05/23/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c1876cfc796b683bfff00b7d137bcfe0b7162c78
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973868"
---
# <a name="convert-a-trial-subscription-to-paid-using-partner-center-apis"></a><span data-ttu-id="1b1cf-103">Api'leri kullanarak deneme aboneliğini İş Ortağı Merkezi dönüştürme</span><span class="sxs-lookup"><span data-stu-id="1b1cf-103">Convert a trial subscription to paid using Partner Center APIs</span></span>

<span data-ttu-id="1b1cf-104">Bir deneme aboneliğini ücretliye dönüştürebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1b1cf-104">You can convert a trial subscription to paid.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1b1cf-105">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="1b1cf-105">Prerequisites</span></span>

- <span data-ttu-id="1b1cf-106">kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="1b1cf-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="1b1cf-107">Bu senaryo yalnızca App+User kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="1b1cf-107">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="1b1cf-108">Müşteri kimliği ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="1b1cf-108">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="1b1cf-109">Müşterinin kimliğini bilmiyorsanız bu kimliği panoda [İş Ortağı Merkezi.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="1b1cf-109">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="1b1cf-110">İş Ortağı Merkezi **menüsünden CSP'yi** ve ardından **Müşteriler'i seçin.**</span><span class="sxs-lookup"><span data-stu-id="1b1cf-110">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="1b1cf-111">Müşteri listesinden müşteriyi ve ardından Hesap'ı **seçin.**</span><span class="sxs-lookup"><span data-stu-id="1b1cf-111">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="1b1cf-112">Müşterinin Hesap sayfasında Müşteri Hesabı Bilgileri **bölümünde Microsoft** **Kimliği'ne** bakın.</span><span class="sxs-lookup"><span data-stu-id="1b1cf-112">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="1b1cf-113">Microsoft Kimliği, müşteri kimliği () ile `customer-tenant-id` aynıdır.</span><span class="sxs-lookup"><span data-stu-id="1b1cf-113">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="1b1cf-114">Etkin bir deneme aboneliği için abonelik kimliği.</span><span class="sxs-lookup"><span data-stu-id="1b1cf-114">A subscription ID for an active trial subscription.</span></span>

- <span data-ttu-id="1b1cf-115">Kullanılabilir dönüştürme teklifi.</span><span class="sxs-lookup"><span data-stu-id="1b1cf-115">An available conversion offer.</span></span>

## <a name="convert-a-trial-subscription-to-a-paid-subscription-through-code"></a><span data-ttu-id="1b1cf-116">Kod aracılığıyla deneme aboneliğini ücretli aboneliğe dönüştürme</span><span class="sxs-lookup"><span data-stu-id="1b1cf-116">Convert a trial subscription to a paid subscription through code</span></span>

<span data-ttu-id="1b1cf-117">Bir deneme aboneliğini ücretli bir aboneliğe dönüştürmek için öncelikle kullanılabilir deneme dönüştürmeleri koleksiyonunu alasınız.</span><span class="sxs-lookup"><span data-stu-id="1b1cf-117">To convert a trial subscription to a paid one, you must first obtain a collection of the trial conversions available.</span></span> <span data-ttu-id="1b1cf-118">Ardından, satın almak istediğiniz dönüştürme teklifini seçmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="1b1cf-118">Then, you must choose the conversion offer that you want to purchase.</span></span>

<span data-ttu-id="1b1cf-119">Dönüştürme teklifleri, varsayılan olarak deneme aboneliğiyle aynı sayıda lisansa sahip olan bir miktar belirtir.</span><span class="sxs-lookup"><span data-stu-id="1b1cf-119">The conversion offers will specify a quantity that defaults to the same number of licenses as the trial subscription.</span></span> <span data-ttu-id="1b1cf-120">[**Quantity**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.conversion.quantity) özelliğini satın almak istediğiniz lisans sayısına ayarerek bu miktarı değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1b1cf-120">You can change this quantity by setting the [**Quantity**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.conversion.quantity) property to the number of licenses that you want to purchase.</span></span>

> [!NOTE]
> <span data-ttu-id="1b1cf-121">Satın alınan lisans sayısından bağımsız olarak, denemenin abonelik kimliği satın alınan lisanslar için yeniden kullanılır.</span><span class="sxs-lookup"><span data-stu-id="1b1cf-121">Regardless of the number of licenses purchased, the subscription ID of the trial is reused for the purchased licenses.</span></span> <span data-ttu-id="1b1cf-122">Sonuç olarak, deneme sürümü kaybolur ve satın alma ile değiştirilir.</span><span class="sxs-lookup"><span data-stu-id="1b1cf-122">As a result, the trial in effect disappears and is replaced by the purchase.</span></span>

<span data-ttu-id="1b1cf-123">Bir deneme aboneliğini kod aracılığıyla dönüştürmek için aşağıdaki adımları kullanın:</span><span class="sxs-lookup"><span data-stu-id="1b1cf-123">Use the following steps to convert a trial subscription through code:</span></span>

1. <span data-ttu-id="1b1cf-124">Kullanılabilir abonelik işlemleri için bir arabirim alın.</span><span class="sxs-lookup"><span data-stu-id="1b1cf-124">Get an interface to the subscription operations available.</span></span> <span data-ttu-id="1b1cf-125">Müşteriyi tanımlamanız ve deneme aboneliğinin abonelik tanımlayıcısını belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="1b1cf-125">You must identify the customer and specify the subscription identifier of the trial subscription.</span></span>

    ``` csharp
    var subscriptionOperations = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId);
    ```

2. <span data-ttu-id="1b1cf-126">Kullanılabilir dönüştürme tekliflerinin bir koleksiyonunu elde.</span><span class="sxs-lookup"><span data-stu-id="1b1cf-126">Get a collection of the available conversion offers.</span></span> <span data-ttu-id="1b1cf-127">Bu yönteme ilişkin istek/yanıt hakkında daha fazla bilgi ve ayrıntılar için [bkz. Deneme dönüştürme tekliflerinin listesini al.](get-a-list-of-trial-conversion-offers.md)</span><span class="sxs-lookup"><span data-stu-id="1b1cf-127">For more information and details on the request/response for this method, see [Get a list of trial conversion offers](get-a-list-of-trial-conversion-offers.md).</span></span>

    ``` csharp
    var conversions = subscriptionOperations.Conversions.Get();
    ```

3. <span data-ttu-id="1b1cf-128">Bir dönüştürme teklifi seçin.</span><span class="sxs-lookup"><span data-stu-id="1b1cf-128">Choose a conversion offer.</span></span> <span data-ttu-id="1b1cf-129">Aşağıdaki kod, koleksiyonda ilk dönüştürme teklifini seçer.</span><span class="sxs-lookup"><span data-stu-id="1b1cf-129">The following code chooses the first conversion offer in the collection.</span></span>

    ``` csharp
    var selectedConversion = conversions.Items.ToList()[0];
    ```

4. <span data-ttu-id="1b1cf-130">İsteğe bağlı olarak, satın alınarak lisans sayısını belirtin.</span><span class="sxs-lookup"><span data-stu-id="1b1cf-130">Optionally, specify the number of licenses to purchase.</span></span> <span data-ttu-id="1b1cf-131">Varsayılan değer, deneme aboneliğinde lisans sayısıdır.</span><span class="sxs-lookup"><span data-stu-id="1b1cf-131">The default is the number of licenses in the trial subscription.</span></span>

    ``` csharp
    selectedConversion.Quantity = 10;
    ```

5. <span data-ttu-id="1b1cf-132">Deneme [**aboneliğini**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.create) ücretliye dönüştürmek için Create veya [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.createasync) yöntemini çağırma.</span><span class="sxs-lookup"><span data-stu-id="1b1cf-132">Call the [**Create**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.create) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.createasync) method to convert the trial subscription to paid.</span></span>

    ``` csharp
    var convertResult = subscriptionOperations.Conversions.Create(selectedConversion);
    ```

## <a name="c"></a><span data-ttu-id="1b1cf-133">C\#</span><span class="sxs-lookup"><span data-stu-id="1b1cf-133">C\#</span></span>

<span data-ttu-id="1b1cf-134">Deneme aboneliğini ücretli bir aboneliğe dönüştürmek için:</span><span class="sxs-lookup"><span data-stu-id="1b1cf-134">To convert a trial subscription to a paid one:</span></span>

1. <span data-ttu-id="1b1cf-135">Müşteriyi [**tanımlamak için IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini müşteri kimliğiyle birlikte kullanın.</span><span class="sxs-lookup"><span data-stu-id="1b1cf-135">Use the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span>

2. <span data-ttu-id="1b1cf-136">Deneme aboneliği kimliğiyle [**Subscriptions.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) yöntemini çağırarak abonelik işlemlerine bir arabirim alın.</span><span class="sxs-lookup"><span data-stu-id="1b1cf-136">Get an interface to subscription operations by calling the [**Subscriptions.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method with the trial subscription ID.</span></span> <span data-ttu-id="1b1cf-137">Abonelik işlemleri arabirimine yönelik bir başvuru yerel değişkene kaydedin.</span><span class="sxs-lookup"><span data-stu-id="1b1cf-137">Save a reference to the subscription operations interface in a local variable.</span></span>

3. <span data-ttu-id="1b1cf-138">Dönüştürmeler [**üzerinde**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.conversions) kullanılabilir işlemlere bir arabirim elde etmek için Dönüştürmeler özelliğini kullanın ve ardından kullanılabilir Dönüştürme tekliflerinin koleksiyonunu almak için [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.get) veya [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.getasync) [**yöntemini**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.conversion) çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1b1cf-138">Use the [**Conversions**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.conversions) property to obtain an interface to the available operations on conversions, and then call the [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.getasync) method to retrieve a collection of available [**Conversion**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.conversion) offers.</span></span> <span data-ttu-id="1b1cf-139">Birini seçmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="1b1cf-139">You must choose one.</span></span> <span data-ttu-id="1b1cf-140">Aşağıdaki örnek varsayılan olarak kullanılabilir ilk dönüştürmeyi kullanır.</span><span class="sxs-lookup"><span data-stu-id="1b1cf-140">The following example defaults to the first conversion available.</span></span>

4. <span data-ttu-id="1b1cf-141">Dönüştürmeler üzerinde kullanılabilir işlemlere bir arabirim elde etmek için, yerel değişkene kaydedilmiş abonelik işlemleri arabirimine başvuru ve [**Dönüştürmeler**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.conversions) özelliğini kullanın.</span><span class="sxs-lookup"><span data-stu-id="1b1cf-141">Use the reference to the subscription operations interface that you saved in a local variable and the [**Conversions**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.conversions) property to obtain an interface to the available operations on conversions.</span></span>

5. <span data-ttu-id="1b1cf-142">Deneme dönüştürmeyi denemesi için seçilen dönüştürme teklifi nesnesini [**Create**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.create) [**veya CreateAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.createasync) yöntemine iletir.</span><span class="sxs-lookup"><span data-stu-id="1b1cf-142">Pass the selected conversion offer object to the [**Create**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.create) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.createasync) method to attempt the trial conversion.</span></span>

### <a name="c-example"></a><span data-ttu-id="1b1cf-143">C \# örneği</span><span class="sxs-lookup"><span data-stu-id="1b1cf-143">C\# example</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string subscriptionId;

// Get subscription operations for the trial subscription.
var subscriptionOperations = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId);

// Get the available conversions.
var conversions = subscriptionOperations.Conversions.Get();

// If there are no conversions available, we&#39;re done.
// Otherwise, convert the trial to the first available conversion offer.
if (conversions.TotalCount <= 0)
{
    System.Console.WriteLine("This subscription has no conversions");
}
else
{
    // Default to the first conversion.
    var selectedConversion = conversions.Items.ToList()[0];

    // Convert the trial and return the result.
    var convertResult = subscriptionOperations.Conversions.Create(selectedConversion);
}
```

## <a name="rest-request"></a><span data-ttu-id="1b1cf-144">REST isteği</span><span class="sxs-lookup"><span data-stu-id="1b1cf-144">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="1b1cf-145">İstek söz dizimi</span><span class="sxs-lookup"><span data-stu-id="1b1cf-145">Request syntax</span></span>

| <span data-ttu-id="1b1cf-146">Yöntem</span><span class="sxs-lookup"><span data-stu-id="1b1cf-146">Method</span></span>   | <span data-ttu-id="1b1cf-147">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="1b1cf-147">Request URI</span></span>                                                                                                                 |
|----------|-----------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="1b1cf-148">**Yayınla**</span><span class="sxs-lookup"><span data-stu-id="1b1cf-148">**POST**</span></span> | <span data-ttu-id="1b1cf-149">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions/{subscription-id}/conversions HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="1b1cf-149">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions/{subscription-id}/conversions HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="1b1cf-150">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="1b1cf-150">URI parameter</span></span>

<span data-ttu-id="1b1cf-151">Müşteri ve deneme aboneliğini tanımlamak için aşağıdaki yol parametrelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="1b1cf-151">Use the following path parameters to identify the customer and trial subscription.</span></span>

| <span data-ttu-id="1b1cf-152">Ad</span><span class="sxs-lookup"><span data-stu-id="1b1cf-152">Name</span></span>            | <span data-ttu-id="1b1cf-153">Tür</span><span class="sxs-lookup"><span data-stu-id="1b1cf-153">Type</span></span>   | <span data-ttu-id="1b1cf-154">Gerekli</span><span class="sxs-lookup"><span data-stu-id="1b1cf-154">Required</span></span> | <span data-ttu-id="1b1cf-155">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1b1cf-155">Description</span></span>                                                     |
|-----------------|--------|----------|-----------------------------------------------------------------|
| <span data-ttu-id="1b1cf-156">customer-id</span><span class="sxs-lookup"><span data-stu-id="1b1cf-156">customer-id</span></span>     | <span data-ttu-id="1b1cf-157">string</span><span class="sxs-lookup"><span data-stu-id="1b1cf-157">string</span></span> | <span data-ttu-id="1b1cf-158">Yes</span><span class="sxs-lookup"><span data-stu-id="1b1cf-158">Yes</span></span>      | <span data-ttu-id="1b1cf-159">Müşteriyi tanımlayan GUID biçimli bir dize.</span><span class="sxs-lookup"><span data-stu-id="1b1cf-159">A GUID formatted string that identifies the customer.</span></span>           |
| <span data-ttu-id="1b1cf-160">subscription-id</span><span class="sxs-lookup"><span data-stu-id="1b1cf-160">subscription-id</span></span> | <span data-ttu-id="1b1cf-161">string</span><span class="sxs-lookup"><span data-stu-id="1b1cf-161">string</span></span> | <span data-ttu-id="1b1cf-162">Yes</span><span class="sxs-lookup"><span data-stu-id="1b1cf-162">Yes</span></span>      | <span data-ttu-id="1b1cf-163">Deneme aboneliğini tanımlayan GUID biçimli bir dize.</span><span class="sxs-lookup"><span data-stu-id="1b1cf-163">A GUID formatted string that identifies the trial subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="1b1cf-164">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="1b1cf-164">Request headers</span></span>

<span data-ttu-id="1b1cf-165">Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="1b1cf-165">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="1b1cf-166">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="1b1cf-166">Request body</span></span>

<span data-ttu-id="1b1cf-167">İstek [gövdesine](conversions-resources.md#conversion) doldurulmuş bir Dönüştürme kaynağı ek gerekir.</span><span class="sxs-lookup"><span data-stu-id="1b1cf-167">A populated [Conversion](conversions-resources.md#conversion) resource must be included in the request body.</span></span>

### <a name="request-example"></a><span data-ttu-id="1b1cf-168">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="1b1cf-168">Request example</span></span>

```http
POST https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/subscriptions/488745B5-2086-4912-802C-6ABB9F7C3638/conversions HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: bd0cde7f-ba87-4010-8a73-1190b641f2a4
MS-CorrelationId: 8daa6d54-72ab-4d6b-9c7d-9266d3734a47
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 234
Expect: 100-continue

{
    "OfferId": "C0BD2E08-11AC-4836-BDC7-3712E744922F",
    "TargetOfferId": "031C9E47-4802-4248-838E-778FB1D2CC05",
    "OrderId": "D51A052E-043C-4A2A-AA37-2BB938CEF6C1",
    "Quantity": 25,
    "BillingCycle": "monthly",
    "Attributes": {
        "ObjectType": "Conversion"
    }
}
```

## <a name="rest-response"></a><span data-ttu-id="1b1cf-169">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="1b1cf-169">REST response</span></span>

<span data-ttu-id="1b1cf-170">Başarılı olursa yanıt gövdesi bir [ConversionResult kaynağı](conversions-resources.md#conversionresult) içerir.</span><span class="sxs-lookup"><span data-stu-id="1b1cf-170">If successful, the response body contains a [ConversionResult](conversions-resources.md#conversionresult) resource.</span></span>

#### <a name="response-success-and-error-codes"></a><span data-ttu-id="1b1cf-171">Yanıt başarı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="1b1cf-171">Response success and error codes</span></span>

<span data-ttu-id="1b1cf-172">Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="1b1cf-172">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="1b1cf-173">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="1b1cf-173">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="1b1cf-174">Tam liste için bkz. [İş Ortağı Merkezi kodları.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="1b1cf-174">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

#### <a name="response-example"></a><span data-ttu-id="1b1cf-175">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="1b1cf-175">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 211
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 8daa6d54-72ab-4d6b-9c7d-9266d3734a47
MS-RequestId: bd0cde7f-ba87-4010-8a73-1190b641f2a4
MS-CV: kW4GzmhvHEqCq1ls.0
MS-ServerId: 030020643
Date: Thu, 15 Jun 2017 23:10:40 GMT

 {
    "subscriptionId": "488745B5-2086-4912-802C-6ABB9F7C3638",
    "offerId": "C0BD2E08-11AC-4836-BDC7-3712E744922F",
    "targetOfferId": "031C9E47-4802-4248-838E-778FB1D2CC05",
    "attributes": {
        "objectType": "ConversionResult"
    }
}
```
