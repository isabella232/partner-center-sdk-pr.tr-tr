---
title: Deneme aboneliğini ücretli aboneliğe dönüştürme
description: Deneme aboneliğini ücretli bir aboneliğe dönüştürmek için Iş Ortağı Merkezi API 'Lerini nasıl kullanacağınızı öğrenin.
ms.date: 05/23/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 59dcf6caf21d407b2fba4cc8438bc435fda9dc77
ms.sourcegitcommit: a25d4951f25502cdf90cfb974022c5e452205f42
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/04/2020
ms.locfileid: "97770066"
---
# <a name="convert-a-trial-subscription-to-paid-using-partner-center-apis"></a><span data-ttu-id="30b71-103">Deneme aboneliğini Iş Ortağı Merkezi API 'Leri kullanarak ücretli olarak dönüştürme</span><span class="sxs-lookup"><span data-stu-id="30b71-103">Convert a trial subscription to paid using Partner Center APIs</span></span>

<span data-ttu-id="30b71-104">**Uygulama hedefi:**</span><span class="sxs-lookup"><span data-stu-id="30b71-104">**Applies to:**</span></span>

- <span data-ttu-id="30b71-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="30b71-105">Partner Center</span></span>

<span data-ttu-id="30b71-106">Deneme aboneliğini ücretli olarak dönüştürebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="30b71-106">You can convert a trial subscription to paid.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="30b71-107">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="30b71-107">Prerequisites</span></span>

- <span data-ttu-id="30b71-108">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="30b71-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="30b71-109">Bu senaryo yalnızca uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="30b71-109">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="30b71-110">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="30b71-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="30b71-111">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="30b71-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="30b71-112">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="30b71-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="30b71-113">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="30b71-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="30b71-114">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="30b71-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="30b71-115">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="30b71-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="30b71-116">Etkin deneme aboneliği için abonelik KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="30b71-116">A subscription ID for an active trial subscription.</span></span>

- <span data-ttu-id="30b71-117">Kullanılabilir bir dönüştürme teklifi.</span><span class="sxs-lookup"><span data-stu-id="30b71-117">An available conversion offer.</span></span>

## <a name="convert-a-trial-subscription-to-paid-through-code"></a><span data-ttu-id="30b71-118">Deneme aboneliğini, kod üzerinden ücretli olarak dönüştürme</span><span class="sxs-lookup"><span data-stu-id="30b71-118">Convert a trial subscription to paid through code</span></span>

<span data-ttu-id="30b71-119">Deneme aboneliğini ücretli bir sürüme dönüştürmek için, önce kullanılabilir deneme dönüştürmelerinden oluşan bir koleksiyonu edinmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="30b71-119">To convert a trial subscription to a paid one, you must first obtain a collection of the trial conversions available.</span></span> <span data-ttu-id="30b71-120">Ardından, Satın almak istediğiniz dönüştürme teklifini seçmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="30b71-120">Then, you must choose the conversion offer that you want to purchase.</span></span>

<span data-ttu-id="30b71-121">Dönüştürme teklifleri, deneme aboneliğiyle aynı sayıda lisansla varsayılan olarak bir miktar belirtir.</span><span class="sxs-lookup"><span data-stu-id="30b71-121">The conversion offers will specify a quantity that defaults to the same number of licenses as the trial subscription.</span></span> <span data-ttu-id="30b71-122">Bu miktarı, [**Miktar**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.conversion.quantity) özelliğini satın almak istediğiniz lisansların sayısı olarak ayarlayarak değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="30b71-122">You can change this quantity by setting the [**Quantity**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.conversion.quantity) property to the number of licenses that you want to purchase.</span></span>

> [!NOTE]
> <span data-ttu-id="30b71-123">Satın alınan lisans sayısı ne olursa olsun, deneme sürümü abonelik KIMLIĞI satın alınan lisanslar için yeniden kullanılır.</span><span class="sxs-lookup"><span data-stu-id="30b71-123">Regardless of the number of licenses purchased, the subscription ID of the trial is reused for the purchased licenses.</span></span> <span data-ttu-id="30b71-124">Sonuç olarak, etkin olan deneme kaybolur ve satın alma işlemi tarafından değiştirilmiştir.</span><span class="sxs-lookup"><span data-stu-id="30b71-124">As a result, the trial in effect disappears and is replaced by the purchase.</span></span>

<span data-ttu-id="30b71-125">Bir deneme aboneliğini kodla dönüştürmek için aşağıdaki adımları kullanın:</span><span class="sxs-lookup"><span data-stu-id="30b71-125">Use the following steps to convert a trial subscription through code:</span></span>

1. <span data-ttu-id="30b71-126">Kullanılabilir abonelik işlemlerine bir arabirim alın.</span><span class="sxs-lookup"><span data-stu-id="30b71-126">Get an interface to the subscription operations available.</span></span> <span data-ttu-id="30b71-127">Müşteriyi tanımlamalısınız ve deneme aboneliğinin abonelik tanımlayıcısını belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="30b71-127">You must identify the customer and specify the subscription identifier of the trial subscription.</span></span>

    ``` csharp
    var subscriptionOperations = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId);
    ```

2. <span data-ttu-id="30b71-128">Kullanılabilir dönüştürme tekliflerinin bir koleksiyonunu alın.</span><span class="sxs-lookup"><span data-stu-id="30b71-128">Get a collection of the available conversion offers.</span></span> <span data-ttu-id="30b71-129">Bu yöntem için istek/yanıt hakkında daha fazla bilgi ve Ayrıntılar için bkz. [deneme dönüştürme tekliflerinin bir listesini alın](get-a-list-of-trial-conversion-offers.md).</span><span class="sxs-lookup"><span data-stu-id="30b71-129">For more information and details on the request/response for this method, see [Get a list of trial conversion offers](get-a-list-of-trial-conversion-offers.md).</span></span>

    ``` csharp
    var conversions = subscriptionOperations.Conversions.Get();
    ```

3. <span data-ttu-id="30b71-130">Bir dönüştürme teklifi seçin.</span><span class="sxs-lookup"><span data-stu-id="30b71-130">Choose a conversion offer.</span></span> <span data-ttu-id="30b71-131">Aşağıdaki kod, koleksiyondaki ilk dönüştürme teklifini seçer.</span><span class="sxs-lookup"><span data-stu-id="30b71-131">The following code chooses the first conversion offer in the collection.</span></span>

    ``` csharp
    var selectedConversion = conversions.Items.ToList()[0];
    ```

4. <span data-ttu-id="30b71-132">İsteğe bağlı olarak, satın alınabilecek lisansların sayısını belirtin.</span><span class="sxs-lookup"><span data-stu-id="30b71-132">Optionally, specify the number of licenses to purchase.</span></span> <span data-ttu-id="30b71-133">Varsayılan değer, deneme aboneliğindeki lisansların sayısıdır.</span><span class="sxs-lookup"><span data-stu-id="30b71-133">The default is the number of licenses in the trial subscription.</span></span>

    ``` csharp
    selectedConversion.Quantity = 10;
    ```

5. <span data-ttu-id="30b71-134">Deneme aboneliğini ücretli olarak dönüştürmek için [**Create**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.create) veya [**createasync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.createasync) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="30b71-134">Call the [**Create**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.create) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.createasync) method to convert the trial subscription to paid.</span></span>

    ``` csharp
    var convertResult = subscriptionOperations.Conversions.Create(selectedConversion);
    ```

## <a name="c"></a><span data-ttu-id="30b71-135">C\#</span><span class="sxs-lookup"><span data-stu-id="30b71-135">C\#</span></span>

<span data-ttu-id="30b71-136">Deneme aboneliğini ücretli birine dönüştürmek için:</span><span class="sxs-lookup"><span data-stu-id="30b71-136">To convert a trial subscription to a paid one:</span></span>

1. <span data-ttu-id="30b71-137">Müşteriyi tanımlamak için, müşteri KIMLIĞIYLE [**ıaggregatepartner. Customers. Byıd**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini kullanın.</span><span class="sxs-lookup"><span data-stu-id="30b71-137">Use the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span>

2. <span data-ttu-id="30b71-138">Deneme aboneliği KIMLIĞIYLE [**abonelikler. Byıd**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) metodunu çağırarak abonelik işlemlerine yönelik bir arabirim alın.</span><span class="sxs-lookup"><span data-stu-id="30b71-138">Get an interface to subscription operations by calling the [**Subscriptions.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method with the trial subscription ID.</span></span> <span data-ttu-id="30b71-139">Yerel bir değişkende abonelik işlemleri arabirimine bir başvuru kaydedin.</span><span class="sxs-lookup"><span data-stu-id="30b71-139">Save a reference to the subscription operations interface in a local variable.</span></span>

3. <span data-ttu-id="30b71-140">Dönüşümlerde kullanılabilir işlemlere bir arabirim elde etmek için [**dönüşümler**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.conversions) özelliğini kullanın ve ardından kullanılabilir [**dönüştürme**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.conversion) tekliflerinin bir koleksiyonunu almak Için [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.get) veya [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.getasync) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="30b71-140">Use the [**Conversions**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.conversions) property to obtain an interface to the available operations on conversions, and then call the [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.getasync) method to retrieve a collection of available [**Conversion**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.conversion) offers.</span></span> <span data-ttu-id="30b71-141">Birini seçmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="30b71-141">You must choose one.</span></span> <span data-ttu-id="30b71-142">Aşağıdaki örnek varsayılan olarak kullanılabilir ilk dönüştürmeyi alır.</span><span class="sxs-lookup"><span data-stu-id="30b71-142">The following example defaults to the first conversion available.</span></span>

4. <span data-ttu-id="30b71-143">Dönüşümlerdeki kullanılabilir işlemlere bir arabirim elde etmek için yerel bir değişkende kaydettiğiniz abonelik işlemleri arabirimine yönelik başvuruyu ve [**dönüşümler**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.conversions) özelliğini kullanın.</span><span class="sxs-lookup"><span data-stu-id="30b71-143">Use the reference to the subscription operations interface that you saved in a local variable and the [**Conversions**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.conversions) property to obtain an interface to the available operations on conversions.</span></span>

5. <span data-ttu-id="30b71-144">Deneme dönüşümünü denemek için seçili dönüştürme teklifini nesnesini [**Create**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.create) veya [**createasync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.createasync) metoduna geçirin.</span><span class="sxs-lookup"><span data-stu-id="30b71-144">Pass the selected conversion offer object to the [**Create**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.create) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.createasync) method to attempt the trial conversion.</span></span>

### <a name="c-example"></a><span data-ttu-id="30b71-145">C \# örneği</span><span class="sxs-lookup"><span data-stu-id="30b71-145">C\# example</span></span>

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

## <a name="rest-request"></a><span data-ttu-id="30b71-146">REST isteği</span><span class="sxs-lookup"><span data-stu-id="30b71-146">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="30b71-147">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="30b71-147">Request syntax</span></span>

| <span data-ttu-id="30b71-148">Yöntem</span><span class="sxs-lookup"><span data-stu-id="30b71-148">Method</span></span>   | <span data-ttu-id="30b71-149">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="30b71-149">Request URI</span></span>                                                                                                                 |
|----------|-----------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="30b71-150">**Yayınla**</span><span class="sxs-lookup"><span data-stu-id="30b71-150">**POST**</span></span> | <span data-ttu-id="30b71-151">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-id}/Subscriptions/{Subscription-id}/dönüşümler http/1.1</span><span class="sxs-lookup"><span data-stu-id="30b71-151">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions/{subscription-id}/conversions HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="30b71-152">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="30b71-152">URI parameter</span></span>

<span data-ttu-id="30b71-153">Müşteri ve deneme aboneliğini belirlemek için aşağıdaki yol parametrelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="30b71-153">Use the following path parameters to identify the customer and trial subscription.</span></span>

| <span data-ttu-id="30b71-154">Ad</span><span class="sxs-lookup"><span data-stu-id="30b71-154">Name</span></span>            | <span data-ttu-id="30b71-155">Tür</span><span class="sxs-lookup"><span data-stu-id="30b71-155">Type</span></span>   | <span data-ttu-id="30b71-156">Gerekli</span><span class="sxs-lookup"><span data-stu-id="30b71-156">Required</span></span> | <span data-ttu-id="30b71-157">Açıklama</span><span class="sxs-lookup"><span data-stu-id="30b71-157">Description</span></span>                                                     |
|-----------------|--------|----------|-----------------------------------------------------------------|
| <span data-ttu-id="30b71-158">müşteri kimliği</span><span class="sxs-lookup"><span data-stu-id="30b71-158">customer-id</span></span>     | <span data-ttu-id="30b71-159">string</span><span class="sxs-lookup"><span data-stu-id="30b71-159">string</span></span> | <span data-ttu-id="30b71-160">Yes</span><span class="sxs-lookup"><span data-stu-id="30b71-160">Yes</span></span>      | <span data-ttu-id="30b71-161">Müşteriyi tanımlayan GUID biçimli dize.</span><span class="sxs-lookup"><span data-stu-id="30b71-161">A GUID formatted string that identifies the customer.</span></span>           |
| <span data-ttu-id="30b71-162">abonelik kimliği</span><span class="sxs-lookup"><span data-stu-id="30b71-162">subscription-id</span></span> | <span data-ttu-id="30b71-163">string</span><span class="sxs-lookup"><span data-stu-id="30b71-163">string</span></span> | <span data-ttu-id="30b71-164">Yes</span><span class="sxs-lookup"><span data-stu-id="30b71-164">Yes</span></span>      | <span data-ttu-id="30b71-165">Deneme aboneliğini tanımlayan GUID biçimli dize.</span><span class="sxs-lookup"><span data-stu-id="30b71-165">A GUID formatted string that identifies the trial subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="30b71-166">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="30b71-166">Request headers</span></span>

<span data-ttu-id="30b71-167">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="30b71-167">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="30b71-168">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="30b71-168">Request body</span></span>

<span data-ttu-id="30b71-169">İstek gövdesine doldurulmuş bir [dönüştürme](conversions-resources.md#conversion) kaynağı eklenmelidir.</span><span class="sxs-lookup"><span data-stu-id="30b71-169">A populated [Conversion](conversions-resources.md#conversion) resource must be included in the request body.</span></span>

### <a name="request-example"></a><span data-ttu-id="30b71-170">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="30b71-170">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="30b71-171">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="30b71-171">REST response</span></span>

<span data-ttu-id="30b71-172">Başarılı olursa, yanıt gövdesi bir [Conversionresult](conversions-resources.md#conversionresult) kaynağı içerir.</span><span class="sxs-lookup"><span data-stu-id="30b71-172">If successful, the response body contains a [ConversionResult](conversions-resources.md#conversionresult) resource.</span></span>

#### <a name="response-success-and-error-codes"></a><span data-ttu-id="30b71-173">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="30b71-173">Response success and error codes</span></span>

<span data-ttu-id="30b71-174">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="30b71-174">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="30b71-175">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="30b71-175">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="30b71-176">Tam liste için bkz. [Partner Center hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="30b71-176">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

#### <a name="response-example"></a><span data-ttu-id="30b71-177">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="30b71-177">Response example</span></span>

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
