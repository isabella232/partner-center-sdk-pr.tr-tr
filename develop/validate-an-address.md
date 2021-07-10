---
title: Bir adresi doğrulama
description: Adres doğrulama API 'sini kullanarak bir adresi doğrulama.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 2eeca91b0e5a507dac6df4ecf61a56aed2d2d921
ms.sourcegitcommit: 51237e7e98d71a7e0590b4d6a4034b6409542126
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/09/2021
ms.locfileid: "113572089"
---
# <a name="validate-an-address"></a><span data-ttu-id="e66fe-103">Bir adresi doğrulama</span><span class="sxs-lookup"><span data-stu-id="e66fe-103">Validate an address</span></span>

<span data-ttu-id="e66fe-104">**Uygulama hedefi**: Iş Ortağı Merkezi | 21Vianet tarafından işletilen iş ortağı Merkezi | Microsoft Bulut Almanya için iş ortağı Merkezi | Microsoft Cloud for US Government için iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="e66fe-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="e66fe-105">Adres doğrulama API 'sini kullanarak bir adresi doğrulama.</span><span class="sxs-lookup"><span data-stu-id="e66fe-105">How to validate an address using the address validation API.</span></span>

<span data-ttu-id="e66fe-106">Adres doğrulama API 'SI yalnızca müşteri profili güncelleştirmelerinin ön doğrulaması için kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="e66fe-106">The address validation API should only be used for pre-validation of customer profile updates.</span></span> <span data-ttu-id="e66fe-107">Ülke Birleşik Devletler, Kanada, Çin veya Meksika olduğunda, eyalet alanının ilgili ülke için geçerli durumlar listesine göre doğrulanacağını anlamak için bunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="e66fe-107">Use it with the understanding that if the country is the United States, Canada, China, or Mexico, the state field is validated against a list of valid states for the respective country.</span></span> <span data-ttu-id="e66fe-108">Diğer tüm ülkelerde, bu test oluşmaz ve API yalnızca durumun geçerli bir dize olduğunu denetler.</span><span class="sxs-lookup"><span data-stu-id="e66fe-108">In all other countries, this test does not occur, and the API only checks that the state is a valid string.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e66fe-109">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="e66fe-109">Prerequisites</span></span>

<span data-ttu-id="e66fe-110">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="e66fe-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="e66fe-111">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="e66fe-111">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="e66fe-112">C\#</span><span class="sxs-lookup"><span data-stu-id="e66fe-112">C\#</span></span>

<span data-ttu-id="e66fe-113">Bir adresi doğrulamak için önce yeni bir **Adres** nesnesi örneği oluşturun ve doğrulanacak adresle doldurun.</span><span class="sxs-lookup"><span data-stu-id="e66fe-113">To validate an address, first instantiate a new **Address** object and populate it with the address to validate.</span></span> <span data-ttu-id="e66fe-114">Ardından, **ıaggregatepartner. doğrulamaları** özelliğinden **doğrulama** işlemlerine bir arabirim alın ve adres nesnesiyle **ısaddressvalid** yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="e66fe-114">Then, retrieve an interface to **Validations** operations from the **IAggregatePartner.Validations** property, and call the **IsAddressValid** method with the address object.</span></span>

```csharp
IAggregatePartner partnerOperations;

// Create an address to validate.
Address address = new Address()
{
    AddressLine1 = "One Microsoft Way",
    City = "Redmond",
    State = "WA",
    PostalCode = "98052",
    Country = "US"
};

// Validate the address.
AddressValidationResponse result = partnerOperations.Validations.IsAddressValid(address);

// If the request completes successfully, you can inspect the response object.

// See the status of the validation.
Console.WriteLine($"Status: {addressValidationResult.Status}");

// See the validation message returned.
Console.WriteLine($"Validation Message Returned: {addressValidationResult.ValidationMessage ?? "No message returned."}");

// See the original address submitted for validation.
Console.WriteLine($"Original Address:\n{this.DisplayAddress(addressValidationResult.OriginalAddress)}");

// See the suggested addresses returned by the API, if any exist.
Console.WriteLine($"Suggested Addresses Returned: {addressValidationResult.SuggestedAddresses?.Count ?? "None."}");

if (addressValidationResult.SuggestedAddresses != null && addressValidationResult.SuggestedAddresses.Any())
{
    addressValidationResult.SuggestedAddresses.ForEach(a => Console.WriteLine(this.DisplayAddress(a)));
}

// Helper method to pretty-print an Address object.
private string DisplayAddress(Address address)
{
    StringBuilder sb = new StringBuilder();

    foreach (var property in address.GetType().GetProperties())
    {
        sb.AppendLine($"{property.Name}: {property.GetValue(address) ?? "None to Display."}");
    }

    return sb.ToString();
}
```

## <a name="rest-request"></a><span data-ttu-id="e66fe-115">REST isteği</span><span class="sxs-lookup"><span data-stu-id="e66fe-115">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="e66fe-116">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="e66fe-116">Request syntax</span></span>

| <span data-ttu-id="e66fe-117">Yöntem</span><span class="sxs-lookup"><span data-stu-id="e66fe-117">Method</span></span>   | <span data-ttu-id="e66fe-118">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="e66fe-118">Request URI</span></span>                                                                 |
|----------|-----------------------------------------------------------------------------|
| <span data-ttu-id="e66fe-119">**Yayınla**</span><span class="sxs-lookup"><span data-stu-id="e66fe-119">**POST**</span></span> | <span data-ttu-id="e66fe-120">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/validations/Address http/1.1</span><span class="sxs-lookup"><span data-stu-id="e66fe-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/validations/address HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="e66fe-121">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="e66fe-121">Request headers</span></span>

<span data-ttu-id="e66fe-122">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="e66fe-122">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="e66fe-123">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="e66fe-123">Request body</span></span>

<span data-ttu-id="e66fe-124">Bu tabloda, istek gövdesinde gereken özellikler açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="e66fe-124">This table describes the required properties in the request body.</span></span>

| <span data-ttu-id="e66fe-125">Ad</span><span class="sxs-lookup"><span data-stu-id="e66fe-125">Name</span></span>         | <span data-ttu-id="e66fe-126">Tür</span><span class="sxs-lookup"><span data-stu-id="e66fe-126">Type</span></span>   | <span data-ttu-id="e66fe-127">Gerekli</span><span class="sxs-lookup"><span data-stu-id="e66fe-127">Required</span></span> | <span data-ttu-id="e66fe-128">Açıklama</span><span class="sxs-lookup"><span data-stu-id="e66fe-128">Description</span></span>                                                |
|--------------|--------|----------|------------------------------------------------------------|
| <span data-ttu-id="e66fe-129">addressline1</span><span class="sxs-lookup"><span data-stu-id="e66fe-129">addressline1</span></span> | <span data-ttu-id="e66fe-130">string</span><span class="sxs-lookup"><span data-stu-id="e66fe-130">string</span></span> | <span data-ttu-id="e66fe-131">Y</span><span class="sxs-lookup"><span data-stu-id="e66fe-131">Y</span></span>        | <span data-ttu-id="e66fe-132">Adresin ilk satırı.</span><span class="sxs-lookup"><span data-stu-id="e66fe-132">The first line of the address.</span></span>                             |
| <span data-ttu-id="e66fe-133">addressline2</span><span class="sxs-lookup"><span data-stu-id="e66fe-133">addressline2</span></span> | <span data-ttu-id="e66fe-134">string</span><span class="sxs-lookup"><span data-stu-id="e66fe-134">string</span></span> | <span data-ttu-id="e66fe-135">N</span><span class="sxs-lookup"><span data-stu-id="e66fe-135">N</span></span>        | <span data-ttu-id="e66fe-136">Adresin ikinci satırı.</span><span class="sxs-lookup"><span data-stu-id="e66fe-136">The second line of the address.</span></span> <span data-ttu-id="e66fe-137">Bu özellik isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="e66fe-137">This property is optional.</span></span> |
| <span data-ttu-id="e66fe-138">city</span><span class="sxs-lookup"><span data-stu-id="e66fe-138">city</span></span>         | <span data-ttu-id="e66fe-139">string</span><span class="sxs-lookup"><span data-stu-id="e66fe-139">string</span></span> | <span data-ttu-id="e66fe-140">Y</span><span class="sxs-lookup"><span data-stu-id="e66fe-140">Y</span></span>        | <span data-ttu-id="e66fe-141">Şehir.</span><span class="sxs-lookup"><span data-stu-id="e66fe-141">The city.</span></span>                                                  |
| <span data-ttu-id="e66fe-142">state</span><span class="sxs-lookup"><span data-stu-id="e66fe-142">state</span></span>        | <span data-ttu-id="e66fe-143">string</span><span class="sxs-lookup"><span data-stu-id="e66fe-143">string</span></span> | <span data-ttu-id="e66fe-144">Y</span><span class="sxs-lookup"><span data-stu-id="e66fe-144">Y</span></span>        | <span data-ttu-id="e66fe-145">Durum.</span><span class="sxs-lookup"><span data-stu-id="e66fe-145">The state.</span></span>                                                 |
| <span data-ttu-id="e66fe-146">PostalCode</span><span class="sxs-lookup"><span data-stu-id="e66fe-146">postalcode</span></span>   | <span data-ttu-id="e66fe-147">string</span><span class="sxs-lookup"><span data-stu-id="e66fe-147">string</span></span> | <span data-ttu-id="e66fe-148">Y</span><span class="sxs-lookup"><span data-stu-id="e66fe-148">Y</span></span>        | <span data-ttu-id="e66fe-149">Posta kodu.</span><span class="sxs-lookup"><span data-stu-id="e66fe-149">The postal code.</span></span>                                           |
| <span data-ttu-id="e66fe-150">ülke</span><span class="sxs-lookup"><span data-stu-id="e66fe-150">country</span></span>      | <span data-ttu-id="e66fe-151">string</span><span class="sxs-lookup"><span data-stu-id="e66fe-151">string</span></span> | <span data-ttu-id="e66fe-152">Y</span><span class="sxs-lookup"><span data-stu-id="e66fe-152">Y</span></span>        | <span data-ttu-id="e66fe-153">İki karakterlik ISO Alpha-2 ülke kodu.</span><span class="sxs-lookup"><span data-stu-id="e66fe-153">The two-character ISO alpha-2 country code.</span></span>                |

### <a name="response-details"></a><span data-ttu-id="e66fe-154">Yanıt ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="e66fe-154">Response details</span></span>

<span data-ttu-id="e66fe-155">Yanıt aşağıdaki durum iletilerinden birini döndürür:</span><span class="sxs-lookup"><span data-stu-id="e66fe-155">The response will return one of the following status messages:</span></span>

| <span data-ttu-id="e66fe-156">Durum</span><span class="sxs-lookup"><span data-stu-id="e66fe-156">Status</span></span>     | <span data-ttu-id="e66fe-157">Açıklama</span><span class="sxs-lookup"><span data-stu-id="e66fe-157">Description</span></span> |    <span data-ttu-id="e66fe-158">Döndürülen önerilen adreslerin sayısı</span><span class="sxs-lookup"><span data-stu-id="e66fe-158">Number of suggested addresses returned</span></span> |
|-------|---------------|-------------------|
|<span data-ttu-id="e66fe-159">Doğrulanan sevk özellikli</span><span class="sxs-lookup"><span data-stu-id="e66fe-159">Verified shippable</span></span> | <span data-ttu-id="e66fe-160">Adres doğrulanır ve sevk edilebilir.</span><span class="sxs-lookup"><span data-stu-id="e66fe-160">Address is verified and can be shipped to.</span></span> | <span data-ttu-id="e66fe-161">Tek</span><span class="sxs-lookup"><span data-stu-id="e66fe-161">Single</span></span> |
|<span data-ttu-id="e66fe-162">Doğrulanamayan</span><span class="sxs-lookup"><span data-stu-id="e66fe-162">Verified</span></span> | <span data-ttu-id="e66fe-163">Adres doğrulandı.</span><span class="sxs-lookup"><span data-stu-id="e66fe-163">Address is verified.</span></span> | <span data-ttu-id="e66fe-164">Tek</span><span class="sxs-lookup"><span data-stu-id="e66fe-164">Single</span></span> |
|<span data-ttu-id="e66fe-165">Etkileşim gerekli</span><span class="sxs-lookup"><span data-stu-id="e66fe-165">Interaction required</span></span> | <span data-ttu-id="e66fe-166">Önerilen adres önemli ölçüde değiştirildi ve kullanıcı onayı gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="e66fe-166">Suggested address has been changed significantly and needs user confirmation.</span></span> | <span data-ttu-id="e66fe-167">Tek</span><span class="sxs-lookup"><span data-stu-id="e66fe-167">Single</span></span> |
|<span data-ttu-id="e66fe-168">Cadde kısmi</span><span class="sxs-lookup"><span data-stu-id="e66fe-168">Street partial</span></span> | <span data-ttu-id="e66fe-169">Adreste verilen cadde kısmi ve daha fazla bilgi gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="e66fe-169">The given street in the address is partial and needs more info.</span></span> | <span data-ttu-id="e66fe-170">Birden çok — en fazla üç</span><span class="sxs-lookup"><span data-stu-id="e66fe-170">Multiple—maximum of three</span></span> |
|<span data-ttu-id="e66fe-171">Şirket içi kısmi</span><span class="sxs-lookup"><span data-stu-id="e66fe-171">Premises partial</span></span> | <span data-ttu-id="e66fe-172">Verilen şirket içi (bina numarası, paket numarası ve diğerleri) kısmi ve daha fazla bilgi gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="e66fe-172">The given premises (building number, suite number, and others) are partial and need more info.</span></span> | <span data-ttu-id="e66fe-173">Birden çok — en fazla üç</span><span class="sxs-lookup"><span data-stu-id="e66fe-173">Multiple—maximum of three</span></span> |
|<span data-ttu-id="e66fe-174">Birden çok</span><span class="sxs-lookup"><span data-stu-id="e66fe-174">Multiple</span></span> | <span data-ttu-id="e66fe-175">Adreste kısmi olan birden çok alan vardır (büyük olasılıkla cadde kısmi ve şirket içi kısmı da dahil).</span><span class="sxs-lookup"><span data-stu-id="e66fe-175">There are multiple fields that are partial in the address (potentially also including street partial and premises partial).</span></span> | <span data-ttu-id="e66fe-176">Birden çok — en fazla üç</span><span class="sxs-lookup"><span data-stu-id="e66fe-176">Multiple—maximum of three</span></span> |
|<span data-ttu-id="e66fe-177">Hiçbiri</span><span class="sxs-lookup"><span data-stu-id="e66fe-177">None</span></span> | <span data-ttu-id="e66fe-178">Adres yanlış.</span><span class="sxs-lookup"><span data-stu-id="e66fe-178">Address is incorrect.</span></span> | <span data-ttu-id="e66fe-179">Hiçbiri</span><span class="sxs-lookup"><span data-stu-id="e66fe-179">None</span></span> |
|<span data-ttu-id="e66fe-180">Doğrulanmamış</span><span class="sxs-lookup"><span data-stu-id="e66fe-180">Not validated</span></span> | <span data-ttu-id="e66fe-181">Adres, doğrulama işlemi aracılığıyla gönderilemedi.</span><span class="sxs-lookup"><span data-stu-id="e66fe-181">Address was not able to be sent through the validation process.</span></span> | <span data-ttu-id="e66fe-182">Hiçbiri</span><span class="sxs-lookup"><span data-stu-id="e66fe-182">None</span></span> |

### <a name="request-example"></a><span data-ttu-id="e66fe-183">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="e66fe-183">Request example</span></span>

```http
# "VerifiedShippable" Request Example

POST https://api.partnercenter.microsoft.com/v1/validations/address HTTP/1.1
Accept: application/json
Content-Type: application/json
Authorization: Bearer <token>
MS-CorrelationId: 29624f3c-90cb-4d34-a7e9-bd2de6d35218
MS-RequestId: eb55c2b8-6f4b-4b44-9557-f76df624b8c0
Host: api.partnercenter.microsoft.com
Content-Length: 137
X-Locale: en-US

{
    "AddressLine1": "1 Microsoft Way",
    "City": "Redmond",
    "State": "WA",
    "PostalCode": "98052",
    "Country": "US"
}

# "StreetPartial" Request Example

POST https://api.partnercenter.microsoft.com/v1/validations/address HTTP/1.1
Accept: application/json
Content-Type: application/json
Authorization: Bearer <token>
MS-CorrelationId: 2c95c9bc-fdfb-4c6a-84f4-57c9b0826b43
MS-RequestId: ee6cf74c-3ab5-48d6-9269-4a4b75bd59dc
Host: api.partnercenter.microsoft.com
Content-Length: 135
X-Locale: en-US

{
    "AddressLine1": "Microsoft Way",
    "City": "Redmond",
    "State": "WA",
    "PostalCode": "98052",
    "Country": "US"
}
```

## <a name="rest-response"></a><span data-ttu-id="e66fe-184">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="e66fe-184">REST response</span></span>

<span data-ttu-id="e66fe-185">Başarılı olursa, yöntem yanıt gövdesinde bir **Addressvalidationresponse** nesnesi döndürür ve **http 200** durum kodudur.</span><span class="sxs-lookup"><span data-stu-id="e66fe-185">If successful, the method returns an **AddressValidationResponse** object in the response body, with a **HTTP 200** status code.</span></span> <span data-ttu-id="e66fe-186">Aşağıda bir örnek gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="e66fe-186">An example is shown below.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="e66fe-187">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="e66fe-187">Response success and error codes</span></span>

<span data-ttu-id="e66fe-188">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="e66fe-188">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="e66fe-189">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="e66fe-189">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="e66fe-190">Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="e66fe-190">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="e66fe-191">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="e66fe-191">Response example</span></span>

```http
# "VerifiedShippable" Response Example

HTTP/1.1 200 OK
Date: Mon, 17 May 2021 23:19:19 GMT
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 29624f3c-90cb-4d34-a7e9-bd2de6d35218
MS-RequestId: eb55c2b8-6f4b-4b44-9557-f76df624b8c0
X-Locale: en-US
 
{
    "originalAddress": {
        "country": "US",
        "city": "Redmond",
        "state": "WA",
        "addressLine1": "1 Microsoft Way",
        "postalCode": "98052"
    },
    "suggestedAddresses": [
        {
            "country": "US",
            "city": "Redmond",
            "state": "WA",
            "addressLine1": "1 Microsoft Way",
            "postalCode": "98052-8300"
        }
    ],
    "status": "VerifiedShippable"
}

# "StreetPartial" Response Example

HTTP/1.1 200 OK
Date: Mon, 17 May 2021 23:34:08 GMT
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 2c95c9bc-fdfb-4c6a-84f4-57c9b0826b43
MS-RequestId: ee6cf74c-3ab5-48d6-9269-4a4b75bd59dc
X-Locale: en-US
 
{
    "originalAddress": {
        "country": "US",
        "city": "Redmond",
        "state": "WA",
        "addressLine1": "Microsoft Way",
        "postalCode": "98052"
    },
    "suggestedAddresses": [
        {
            "country": "US",
            "city": "Redmond",
            "state": "WA",
            "addressLine1": "1 Microsoft Way",
            "postalCode": "98052-6399"
        }
    ],
    "status": "StreetPartial",
    "validationMessage": "Address field invalid for property: 'Region', 'PostalCode', 'City'"
}
```
