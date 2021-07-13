---
title: Bir adresi doğrulama
description: Adres doğrulama API'sini kullanarak adresi doğrulama.
ms.date: 05/17/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 30f5cd526ab038dce400e79822d89b8086ba3799
ms.sourcegitcommit: 41bf9dca55f4c96d382b327a75b2d2418edfc9bc
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/13/2021
ms.locfileid: "113655615"
---
# <a name="validate-an-address"></a><span data-ttu-id="56635-103">Bir adresi doğrulama</span><span class="sxs-lookup"><span data-stu-id="56635-103">Validate an address</span></span>

<span data-ttu-id="56635-104">**Için geçerlidir:** İş Ortağı Merkezi | İş Ortağı Merkezi 21Vianet | İş Ortağı Merkezi Microsoft Bulut Almanya için | İş Ortağı Merkezi için Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="56635-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="56635-105">Adres doğrulama API'sini kullanarak adresi doğrulama.</span><span class="sxs-lookup"><span data-stu-id="56635-105">How to validate an address using the address validation API.</span></span>

<span data-ttu-id="56635-106">Adres doğrulama API'si yalnızca müşteri profili güncelleştirmelerinin ön doğrulaması için kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="56635-106">The address validation API should only be used for pre-validation of customer profile updates.</span></span> <span data-ttu-id="56635-107">Ülke Birleşik Devletler, Kanada, Çin veya Meksika ise eyalet alanı ilgili ülke için geçerli eyaletler listesinde doğrulanır.</span><span class="sxs-lookup"><span data-stu-id="56635-107">Use it with the understanding that if the country is the United States, Canada, China, or Mexico, the state field is validated against a list of valid states for the respective country.</span></span> <span data-ttu-id="56635-108">Diğer tüm ülkelerde bu test oluşmaz ve API yalnızca durumunun geçerli bir dize olduğunu denetler.</span><span class="sxs-lookup"><span data-stu-id="56635-108">In all other countries, this test does not occur, and the API only checks that the state is a valid string.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="56635-109">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="56635-109">Prerequisites</span></span>

<span data-ttu-id="56635-110">kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="56635-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="56635-111">Bu senaryo hem tek başına Uygulama hem de Uygulama+Kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="56635-111">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="56635-112">C\#</span><span class="sxs-lookup"><span data-stu-id="56635-112">C\#</span></span>

<span data-ttu-id="56635-113">Bir adresi doğrulamak için öncelikle yeni bir **Address** nesnesi örneği oluşturma ve bunu doğrulanması gereken adresle doldurmak.</span><span class="sxs-lookup"><span data-stu-id="56635-113">To validate an address, first instantiate a new **Address** object and populate it with the address to validate.</span></span> <span data-ttu-id="56635-114">Ardından **IAggregatePartner.Validations** özelliğinden **Validations** işlemlerine bir arabirim alın ve adres nesnesiyle **IsAddressValid** yöntemini arayın.</span><span class="sxs-lookup"><span data-stu-id="56635-114">Then, retrieve an interface to **Validations** operations from the **IAggregatePartner.Validations** property, and call the **IsAddressValid** method with the address object.</span></span>

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

## <a name="rest-request"></a><span data-ttu-id="56635-115">REST isteği</span><span class="sxs-lookup"><span data-stu-id="56635-115">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="56635-116">İstek söz dizimi</span><span class="sxs-lookup"><span data-stu-id="56635-116">Request syntax</span></span>

| <span data-ttu-id="56635-117">Yöntem</span><span class="sxs-lookup"><span data-stu-id="56635-117">Method</span></span>   | <span data-ttu-id="56635-118">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="56635-118">Request URI</span></span>                                                                 |
|----------|-----------------------------------------------------------------------------|
| <span data-ttu-id="56635-119">**Yayınla**</span><span class="sxs-lookup"><span data-stu-id="56635-119">**POST**</span></span> | <span data-ttu-id="56635-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/validations/address HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="56635-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/validations/address HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="56635-121">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="56635-121">Request headers</span></span>

<span data-ttu-id="56635-122">Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="56635-122">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="56635-123">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="56635-123">Request body</span></span>

<span data-ttu-id="56635-124">Bu tablo, istek gövdesinde gerekli özellikleri açıklar.</span><span class="sxs-lookup"><span data-stu-id="56635-124">This table describes the required properties in the request body.</span></span>

| <span data-ttu-id="56635-125">Ad</span><span class="sxs-lookup"><span data-stu-id="56635-125">Name</span></span>         | <span data-ttu-id="56635-126">Tür</span><span class="sxs-lookup"><span data-stu-id="56635-126">Type</span></span>   | <span data-ttu-id="56635-127">Gerekli</span><span class="sxs-lookup"><span data-stu-id="56635-127">Required</span></span> | <span data-ttu-id="56635-128">Açıklama</span><span class="sxs-lookup"><span data-stu-id="56635-128">Description</span></span>                                                |
|--------------|--------|----------|------------------------------------------------------------|
| <span data-ttu-id="56635-129">addressline1</span><span class="sxs-lookup"><span data-stu-id="56635-129">addressline1</span></span> | <span data-ttu-id="56635-130">string</span><span class="sxs-lookup"><span data-stu-id="56635-130">string</span></span> | <span data-ttu-id="56635-131">Y</span><span class="sxs-lookup"><span data-stu-id="56635-131">Y</span></span>        | <span data-ttu-id="56635-132">Adresin ilk satırı.</span><span class="sxs-lookup"><span data-stu-id="56635-132">The first line of the address.</span></span>                             |
| <span data-ttu-id="56635-133">Addressline2</span><span class="sxs-lookup"><span data-stu-id="56635-133">addressline2</span></span> | <span data-ttu-id="56635-134">string</span><span class="sxs-lookup"><span data-stu-id="56635-134">string</span></span> | <span data-ttu-id="56635-135">N</span><span class="sxs-lookup"><span data-stu-id="56635-135">N</span></span>        | <span data-ttu-id="56635-136">Adresin ikinci satırı.</span><span class="sxs-lookup"><span data-stu-id="56635-136">The second line of the address.</span></span> <span data-ttu-id="56635-137">Bu özellik isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="56635-137">This property is optional.</span></span> |
| <span data-ttu-id="56635-138">city</span><span class="sxs-lookup"><span data-stu-id="56635-138">city</span></span>         | <span data-ttu-id="56635-139">string</span><span class="sxs-lookup"><span data-stu-id="56635-139">string</span></span> | <span data-ttu-id="56635-140">Y</span><span class="sxs-lookup"><span data-stu-id="56635-140">Y</span></span>        | <span data-ttu-id="56635-141">Şehir.</span><span class="sxs-lookup"><span data-stu-id="56635-141">The city.</span></span>                                                  |
| <span data-ttu-id="56635-142">state</span><span class="sxs-lookup"><span data-stu-id="56635-142">state</span></span>        | <span data-ttu-id="56635-143">string</span><span class="sxs-lookup"><span data-stu-id="56635-143">string</span></span> | <span data-ttu-id="56635-144">Y</span><span class="sxs-lookup"><span data-stu-id="56635-144">Y</span></span>        | <span data-ttu-id="56635-145">Durum.</span><span class="sxs-lookup"><span data-stu-id="56635-145">The state.</span></span>                                                 |
| <span data-ttu-id="56635-146">Postakodu</span><span class="sxs-lookup"><span data-stu-id="56635-146">postalcode</span></span>   | <span data-ttu-id="56635-147">string</span><span class="sxs-lookup"><span data-stu-id="56635-147">string</span></span> | <span data-ttu-id="56635-148">Y</span><span class="sxs-lookup"><span data-stu-id="56635-148">Y</span></span>        | <span data-ttu-id="56635-149">Posta kodu.</span><span class="sxs-lookup"><span data-stu-id="56635-149">The postal code.</span></span>                                           |
| <span data-ttu-id="56635-150">ülke</span><span class="sxs-lookup"><span data-stu-id="56635-150">country</span></span>      | <span data-ttu-id="56635-151">string</span><span class="sxs-lookup"><span data-stu-id="56635-151">string</span></span> | <span data-ttu-id="56635-152">Y</span><span class="sxs-lookup"><span data-stu-id="56635-152">Y</span></span>        | <span data-ttu-id="56635-153">İki karakterli ISO alfa-2 ülke kodu.</span><span class="sxs-lookup"><span data-stu-id="56635-153">The two-character ISO alpha-2 country code.</span></span>                |

### <a name="response-details"></a><span data-ttu-id="56635-154">Yanıt ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="56635-154">Response details</span></span>

<span data-ttu-id="56635-155">Yanıt aşağıdaki durum iletilerinden birini geri dönecektir:</span><span class="sxs-lookup"><span data-stu-id="56635-155">The response will return one of the following status messages:</span></span>

| <span data-ttu-id="56635-156">Durum</span><span class="sxs-lookup"><span data-stu-id="56635-156">Status</span></span>     | <span data-ttu-id="56635-157">Açıklama</span><span class="sxs-lookup"><span data-stu-id="56635-157">Description</span></span> |    <span data-ttu-id="56635-158">Döndürülen önerilen adres sayısı</span><span class="sxs-lookup"><span data-stu-id="56635-158">Number of suggested addresses returned</span></span> |
|-------|---------------|-------------------|
|<span data-ttu-id="56635-159">Doğrulanmış gönderilebilir</span><span class="sxs-lookup"><span data-stu-id="56635-159">Verified shippable</span></span> | <span data-ttu-id="56635-160">Adres doğrulanır ve adresine gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="56635-160">Address is verified and can be shipped to.</span></span> | <span data-ttu-id="56635-161">Tek</span><span class="sxs-lookup"><span data-stu-id="56635-161">Single</span></span> |
|<span data-ttu-id="56635-162">Doğrulandı</span><span class="sxs-lookup"><span data-stu-id="56635-162">Verified</span></span> | <span data-ttu-id="56635-163">Adres doğrulandı.</span><span class="sxs-lookup"><span data-stu-id="56635-163">Address is verified.</span></span> | <span data-ttu-id="56635-164">Tek</span><span class="sxs-lookup"><span data-stu-id="56635-164">Single</span></span> |
|<span data-ttu-id="56635-165">Etkileşim gerekiyor</span><span class="sxs-lookup"><span data-stu-id="56635-165">Interaction required</span></span> | <span data-ttu-id="56635-166">Önerilen adres önemli ölçüde değiştirildi ve kullanıcı onayı gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="56635-166">Suggested address has been changed significantly and needs user confirmation.</span></span> | <span data-ttu-id="56635-167">Tek</span><span class="sxs-lookup"><span data-stu-id="56635-167">Single</span></span> |
|<span data-ttu-id="56635-168">Sokak kısmii</span><span class="sxs-lookup"><span data-stu-id="56635-168">Street partial</span></span> | <span data-ttu-id="56635-169">Adreste verilen sokak kısmidir ve daha fazla bilgiye ihtiyaç vardır.</span><span class="sxs-lookup"><span data-stu-id="56635-169">The given street in the address is partial and needs more info.</span></span> | <span data-ttu-id="56635-170">Çoklu— en fazla üç</span><span class="sxs-lookup"><span data-stu-id="56635-170">Multiple—maximum of three</span></span> |
|<span data-ttu-id="56635-171">Kısmi şirket içi</span><span class="sxs-lookup"><span data-stu-id="56635-171">Premises partial</span></span> | <span data-ttu-id="56635-172">Verilen şirket (bina numarası, paket numarası ve diğerleri) kısmidir ve daha fazla bilgiye ihtiyaç vardır.</span><span class="sxs-lookup"><span data-stu-id="56635-172">The given premises (building number, suite number, and others) are partial and need more info.</span></span> | <span data-ttu-id="56635-173">Çoklu— en fazla üç</span><span class="sxs-lookup"><span data-stu-id="56635-173">Multiple—maximum of three</span></span> |
|<span data-ttu-id="56635-174">Birden çok</span><span class="sxs-lookup"><span data-stu-id="56635-174">Multiple</span></span> | <span data-ttu-id="56635-175">Adreste kısmi olan birden çok alan vardır (kısmi sokak ve kısmi şirket de dahil olmak üzere).</span><span class="sxs-lookup"><span data-stu-id="56635-175">There are multiple fields that are partial in the address (potentially also including street partial and premises partial).</span></span> | <span data-ttu-id="56635-176">Çoklu— en fazla üç</span><span class="sxs-lookup"><span data-stu-id="56635-176">Multiple—maximum of three</span></span> |
|<span data-ttu-id="56635-177">Hiçbiri</span><span class="sxs-lookup"><span data-stu-id="56635-177">None</span></span> | <span data-ttu-id="56635-178">Adres yanlış.</span><span class="sxs-lookup"><span data-stu-id="56635-178">Address is incorrect.</span></span> | <span data-ttu-id="56635-179">Hiçbiri</span><span class="sxs-lookup"><span data-stu-id="56635-179">None</span></span> |
|<span data-ttu-id="56635-180">Doğrulanmamış</span><span class="sxs-lookup"><span data-stu-id="56635-180">Not validated</span></span> | <span data-ttu-id="56635-181">Adres doğrulama işlemi aracılığıyla gönderileemedi.</span><span class="sxs-lookup"><span data-stu-id="56635-181">Address was not able to be sent through the validation process.</span></span> | <span data-ttu-id="56635-182">Hiçbiri</span><span class="sxs-lookup"><span data-stu-id="56635-182">None</span></span> |

### <a name="request-example"></a><span data-ttu-id="56635-183">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="56635-183">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="56635-184">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="56635-184">REST response</span></span>

<span data-ttu-id="56635-185">Başarılı olursa, yöntem http **200** durum koduyla yanıt gövdesinde **bir AddressValidationResponse** nesnesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="56635-185">If successful, the method returns an **AddressValidationResponse** object in the response body, with a **HTTP 200** status code.</span></span> <span data-ttu-id="56635-186">Aşağıda bir örnek gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="56635-186">An example is shown below.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="56635-187">Yanıt başarı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="56635-187">Response success and error codes</span></span>

<span data-ttu-id="56635-188">Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="56635-188">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="56635-189">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="56635-189">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="56635-190">Tam liste için bkz. [İŞ ORTAĞı MERKEZI REST hata kodları.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="56635-190">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="56635-191">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="56635-191">Response example</span></span>

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
