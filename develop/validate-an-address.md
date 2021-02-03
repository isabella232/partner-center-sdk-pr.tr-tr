---
title: Bir adresi doğrulama
description: Adres doğrulama API 'sini kullanarak bir adresi doğrulama.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 22d5faec2fdab4907067bb01cb74e110032dea9a
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768932"
---
# <a name="validate-an-address"></a><span data-ttu-id="ef534-103">Bir adresi doğrulama</span><span class="sxs-lookup"><span data-stu-id="ef534-103">Validate an address</span></span>

<span data-ttu-id="ef534-104">**Uygulama hedefi**</span><span class="sxs-lookup"><span data-stu-id="ef534-104">**Applies To**</span></span>

- <span data-ttu-id="ef534-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="ef534-105">Partner Center</span></span>
- <span data-ttu-id="ef534-106">21Vianet tarafından çalıştırılan iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="ef534-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="ef534-107">Microsoft Bulut Almanya için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="ef534-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="ef534-108">Microsoft Cloud for US Government için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="ef534-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="ef534-109">Adres doğrulama API 'sini kullanarak bir adresi doğrulama.</span><span class="sxs-lookup"><span data-stu-id="ef534-109">How to validate an address using the address validation API.</span></span>

<span data-ttu-id="ef534-110">Adres doğrulama API 'SI yalnızca müşteri profili güncelleştirmelerinin ön doğrulaması için kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ef534-110">The address validation API should only be used for pre-validation of customer profile updates.</span></span> <span data-ttu-id="ef534-111">Ülke Birleşik Devletler, Kanada, Çin veya Meksika olduğunda, eyalet alanının ilgili ülke için geçerli durumlar listesine göre doğrulanacağını anlamak için bunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="ef534-111">Use it with the understanding that if the country is the United States, Canada, China, or Mexico, the state field is validated against a list of valid states for the respective country.</span></span> <span data-ttu-id="ef534-112">Diğer tüm ülkelerde, bu test oluşmaz ve API yalnızca durumun geçerli bir dize olduğunu denetler.</span><span class="sxs-lookup"><span data-stu-id="ef534-112">In all other countries, this test does not occur, and the API only checks that the state is a valid string.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ef534-113">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="ef534-113">Prerequisites</span></span>

<span data-ttu-id="ef534-114">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="ef534-114">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="ef534-115">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="ef534-115">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="ef534-116">C\#</span><span class="sxs-lookup"><span data-stu-id="ef534-116">C\#</span></span>

<span data-ttu-id="ef534-117">Bir adresi doğrulamak için önce yeni bir **Adres** nesnesi örneği oluşturun ve doğrulanacak adresle doldurun.</span><span class="sxs-lookup"><span data-stu-id="ef534-117">To validate an address, first instantiate a new **Address** object and populate it with the address to validate.</span></span> <span data-ttu-id="ef534-118">Ardından, **ıaggregatepartner. doğrulamaları** özelliğinden **doğrulama** işlemlerine bir arabirim alın ve adres nesnesiyle **ısaddressvalid** yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="ef534-118">Then, retrieve an interface to **Validations** operations from the **IAggregatePartner.Validations** property, and call the **IsAddressValid** method with the address object.</span></span>

```csharp
// IAggregatePartner partnerOperations;

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
bool result = partnerOperations.Validations.IsAddressValid(address);

// If the address is valid, the result should equal true.
Console.WriteLine("Result: " + result.ToString());

// The following is an example that causes address validation to fail.
try
{
    // Change to an invalid postal code for this address.
    address.PostalCode = "98007";

    // Validate the address.
    result = partnerOperations.Validations.IsAddressValid(address);

    Console.WriteLine("ERROR: The code should have thrown an exception - BadRequest(400).");
}
catch (PartnerException exception)
{
    if (exception.ErrorCategory == PartnerErrorCategory.BadInput)
    {
        Console.WriteLine(exception.ErrorCategory.ToString());
        Console.WriteLine("Exception:");
        Console.WriteLine("Message: {0}", exception.Message);
    }
    else
    {
        throw;
    }
}
```

## <a name="java"></a><span data-ttu-id="ef534-119">Java</span><span class="sxs-lookup"><span data-stu-id="ef534-119">Java</span></span>

<span data-ttu-id="ef534-120">Bir adresi doğrulamak için önce yeni bir **Adres** nesnesi örneği oluşturun ve doğrulanacak adresle doldurun.</span><span class="sxs-lookup"><span data-stu-id="ef534-120">To validate an address, first instantiate a new **Address** object and populate it with the address to validate.</span></span> <span data-ttu-id="ef534-121">Ardından, **ıaggregatepartner. Getdoğrulamaları** işlevinden **doğrulama** işlemlerine bir arabirim alın ve adres nesnesiyle **ısaddressvalid** yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="ef534-121">Then, retrieve an interface to **Validations** operations from the **IAggregatePartner.getValidations** function, and call the **isAddressValid** method with the address object.</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

```java
// IAggregatePartner partnerOperations;

// Create an address to validate.
Address address = new Address();

address.setAddressLine1("One Microsoft Way");
address.setCity("Redmond");
address.setState("WA");
address.setCountry("US");
address.setPostalCode("98052");

try
{
    // Validate the address
    Boolean validationResult = partnerOperations.getValidations().isAddressValid(address);

    System.out.println(validationResult ? "The address is valid." : "Invalid address");
}
catch (Exception exception)
{
    System.out.println("Address is invalid");

    if (! StringHelper.isNullOrWhiteSpace(exception.getMessage()))
    {
        System.out.println(exception.getMessage());
    }
}
```

## <a name="powershell"></a><span data-ttu-id="ef534-122">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ef534-122">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="ef534-123">Bir adresi doğrulamak için, [**Test-PartnerAddress**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Test-PartnerAddress.md) adresini doldurulmuş adres parametreleriyle yürütün.</span><span class="sxs-lookup"><span data-stu-id="ef534-123">To validate an address, execute the [**Test-PartnerAddress**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Test-PartnerAddress.md) with the address parameters populated.</span></span>

```powershell
Test-PartnerAddress -AddressLine1 '700 Bellevue Way NE' -City 'Bellevue' -Country 'US' -PostalCode '98004' -State 'WA'
```

## <a name="rest-request"></a><span data-ttu-id="ef534-124">REST isteği</span><span class="sxs-lookup"><span data-stu-id="ef534-124">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="ef534-125">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="ef534-125">Request syntax</span></span>

| <span data-ttu-id="ef534-126">Yöntem</span><span class="sxs-lookup"><span data-stu-id="ef534-126">Method</span></span>   | <span data-ttu-id="ef534-127">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="ef534-127">Request URI</span></span>                                                                 |
|----------|-----------------------------------------------------------------------------|
| <span data-ttu-id="ef534-128">**Yayınla**</span><span class="sxs-lookup"><span data-stu-id="ef534-128">**POST**</span></span> | <span data-ttu-id="ef534-129">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/validations/Address http/1.1</span><span class="sxs-lookup"><span data-stu-id="ef534-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/validations/address HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="ef534-130">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="ef534-130">Request headers</span></span>

<span data-ttu-id="ef534-131">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="ef534-131">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="ef534-132">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="ef534-132">Request body</span></span>

<span data-ttu-id="ef534-133">Bu tabloda, istek gövdesinde gereken özellikler açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="ef534-133">This table describes the required properties in the request body.</span></span>

| <span data-ttu-id="ef534-134">Ad</span><span class="sxs-lookup"><span data-stu-id="ef534-134">Name</span></span>         | <span data-ttu-id="ef534-135">Tür</span><span class="sxs-lookup"><span data-stu-id="ef534-135">Type</span></span>   | <span data-ttu-id="ef534-136">Gerekli</span><span class="sxs-lookup"><span data-stu-id="ef534-136">Required</span></span> | <span data-ttu-id="ef534-137">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ef534-137">Description</span></span>                                                |
|--------------|--------|----------|------------------------------------------------------------|
| <span data-ttu-id="ef534-138">addressline1</span><span class="sxs-lookup"><span data-stu-id="ef534-138">addressline1</span></span> | <span data-ttu-id="ef534-139">string</span><span class="sxs-lookup"><span data-stu-id="ef534-139">string</span></span> | <span data-ttu-id="ef534-140">Y</span><span class="sxs-lookup"><span data-stu-id="ef534-140">Y</span></span>        | <span data-ttu-id="ef534-141">Adresin ilk satırı.</span><span class="sxs-lookup"><span data-stu-id="ef534-141">The first line of the address.</span></span>                             |
| <span data-ttu-id="ef534-142">addressline2</span><span class="sxs-lookup"><span data-stu-id="ef534-142">addressline2</span></span> | <span data-ttu-id="ef534-143">string</span><span class="sxs-lookup"><span data-stu-id="ef534-143">string</span></span> | <span data-ttu-id="ef534-144">N</span><span class="sxs-lookup"><span data-stu-id="ef534-144">N</span></span>        | <span data-ttu-id="ef534-145">Adresin ikinci satırı.</span><span class="sxs-lookup"><span data-stu-id="ef534-145">The second line of the address.</span></span> <span data-ttu-id="ef534-146">Bu özellik isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="ef534-146">This property is optional.</span></span> |
| <span data-ttu-id="ef534-147">city</span><span class="sxs-lookup"><span data-stu-id="ef534-147">city</span></span>         | <span data-ttu-id="ef534-148">string</span><span class="sxs-lookup"><span data-stu-id="ef534-148">string</span></span> | <span data-ttu-id="ef534-149">Y</span><span class="sxs-lookup"><span data-stu-id="ef534-149">Y</span></span>        | <span data-ttu-id="ef534-150">Şehir.</span><span class="sxs-lookup"><span data-stu-id="ef534-150">The city.</span></span>                                                  |
| <span data-ttu-id="ef534-151">state</span><span class="sxs-lookup"><span data-stu-id="ef534-151">state</span></span>        | <span data-ttu-id="ef534-152">string</span><span class="sxs-lookup"><span data-stu-id="ef534-152">string</span></span> | <span data-ttu-id="ef534-153">Y</span><span class="sxs-lookup"><span data-stu-id="ef534-153">Y</span></span>        | <span data-ttu-id="ef534-154">Durum.</span><span class="sxs-lookup"><span data-stu-id="ef534-154">The state.</span></span>                                                 |
| <span data-ttu-id="ef534-155">PostalCode</span><span class="sxs-lookup"><span data-stu-id="ef534-155">postalcode</span></span>   | <span data-ttu-id="ef534-156">string</span><span class="sxs-lookup"><span data-stu-id="ef534-156">string</span></span> | <span data-ttu-id="ef534-157">Y</span><span class="sxs-lookup"><span data-stu-id="ef534-157">Y</span></span>        | <span data-ttu-id="ef534-158">Posta kodu.</span><span class="sxs-lookup"><span data-stu-id="ef534-158">The postal code.</span></span>                                           |
| <span data-ttu-id="ef534-159">ülke</span><span class="sxs-lookup"><span data-stu-id="ef534-159">country</span></span>      | <span data-ttu-id="ef534-160">string</span><span class="sxs-lookup"><span data-stu-id="ef534-160">string</span></span> | <span data-ttu-id="ef534-161">Y</span><span class="sxs-lookup"><span data-stu-id="ef534-161">Y</span></span>        | <span data-ttu-id="ef534-162">İki karakterlik ISO Alpha-2 ülke kodu.</span><span class="sxs-lookup"><span data-stu-id="ef534-162">The two-character ISO alpha-2 country code.</span></span>                |

### <a name="request-example"></a><span data-ttu-id="ef534-163">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="ef534-163">Request example</span></span>

```http
POST https://api.partnercenter.microsoft.com/v1/validations/address HTTP/1.1
Content-Type: application/json
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 0b30452a-8be2-4b8b-b25b-2d4850f4345f
MS-CorrelationId: 8a853a1a-b0e6-4cb0-ae87-d6dd32ac3a0c
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Content-Length: 129

{
    "AddressLine1": "One Microsoft Way",
    "City": "Redmond",
    "State": "WA",
    "PostalCode": "98052",
    "Country": "US"
}
```

## <a name="rest-response"></a><span data-ttu-id="ef534-164">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="ef534-164">REST response</span></span>

<span data-ttu-id="ef534-165">Başarılı olursa, yöntemi aşağıda gösterilen yanıt doğrulama başarılı örneğinde gösterildiği gibi 200 durum kodunu döndürür.</span><span class="sxs-lookup"><span data-stu-id="ef534-165">If successful, the method returns a status code 200 as demonstrated in the Response - validation succeeded example shown below.</span></span>

<span data-ttu-id="ef534-166">İstek başarısız olursa, yöntemi aşağıda gösterilen yanıt doğrulama başarısız örnek bölümünde gösterildiği gibi 400 durum kodunu döndürür.</span><span class="sxs-lookup"><span data-stu-id="ef534-166">If the request fails, the method returns a status code 400 as demonstrated in the Response - validation failed example shown below.</span></span> <span data-ttu-id="ef534-167">Yanıt gövdesi, hata hakkında ek bilgi içeren bir JSON yükü içerir.</span><span class="sxs-lookup"><span data-stu-id="ef534-167">The response body contains a JSON payload with additional information about the error.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="ef534-168">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="ef534-168">Response success and error codes</span></span>

<span data-ttu-id="ef534-169">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="ef534-169">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="ef534-170">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="ef534-170">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="ef534-171">Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="ef534-171">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response---validation-succeeded-example"></a><span data-ttu-id="ef534-172">Yanıt-doğrulama başarılı örneği</span><span class="sxs-lookup"><span data-stu-id="ef534-172">Response - validation succeeded example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 0
MS-CorrelationId: 8a853a1a-b0e6-4cb0-ae87-d6dd32ac3a0c
MS-RequestId: 0b30452a-8be2-4b8b-b25b-2d4850f4345f
MS-CV: IqhjoWVyq0Kl81dO.0
MS-ServerId: 030011719
Date: Mon, 13 Mar 2017 23:56:12 GMT
```

### <a name="response---validation-failed-example"></a><span data-ttu-id="ef534-173">Yanıt doğrulama başarısız örnek</span><span class="sxs-lookup"><span data-stu-id="ef534-173">Response - validation failed example</span></span>

```http
HTTP/1.1 400 Bad Request
Content-Length: 418
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 8a853a1a-b0e6-4cb0-ae87-d6dd32ac3a0c
MS-RequestId: 0b30452a-8be2-4b8b-b25b-2d4850f4345f
MS-CV: pdlItMyvtkmGHDWt.0
MS-ServerId: 101112012
Date: Tue, 14 Mar 2017 01:57:55 GMT

{
    "code": 2007,
    "description": "{\"code\":\"60071\",\"reason\":\"ZipCityInvalid - Details: Field - &#39;City&#39; is corrected from OldValue: &#39;Redmond&#39; to NewValue: &#39;BELLEVUE&#39;.\",\"corrected_address\":{\"country\":\"US\",\"region\":\"WA\",\"city\":\"BELLEVUE\",\"address_line1\":\"One Microsoft Way\",\"postal_code\":\"98007\"},\"object_type\":\"AddressValidation\",\"resource_status\":\"Active\"}",
    "data": [],
    "source": "PartnerFD"
}
```
