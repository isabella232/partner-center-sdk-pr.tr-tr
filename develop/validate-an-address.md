---
title: Bir adresi doğrulama
description: Adres doğrulama API'sini kullanarak adresi doğrulama.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 14d45977f3af6e8bba1b7cb7f969aa7c5bb671da
ms.sourcegitcommit: 4275f9f67f9479ce27af6a9fda96fe86d0bc0b44
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/05/2021
ms.locfileid: "111529894"
---
# <a name="validate-an-address"></a><span data-ttu-id="58f67-103">Bir adresi doğrulama</span><span class="sxs-lookup"><span data-stu-id="58f67-103">Validate an address</span></span>

<span data-ttu-id="58f67-104">**Için geçerlidir:** İş Ortağı Merkezi | İş Ortağı Merkezi 21Vianet | İş Ortağı Merkezi Microsoft Bulut Almanya için | İş Ortağı Merkezi için Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="58f67-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="58f67-105">Adres doğrulama API'sini kullanarak adresi doğrulama.</span><span class="sxs-lookup"><span data-stu-id="58f67-105">How to validate an address using the address validation API.</span></span>

<span data-ttu-id="58f67-106">Adres doğrulama API'si yalnızca müşteri profili güncelleştirmelerinin ön doğrulaması için kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="58f67-106">The address validation API should only be used for pre-validation of customer profile updates.</span></span> <span data-ttu-id="58f67-107">Ülke Birleşik Devletler, Kanada, Çin veya Meksika ise eyalet alanı ilgili ülke için geçerli eyaletler listesinde doğrulanır.</span><span class="sxs-lookup"><span data-stu-id="58f67-107">Use it with the understanding that if the country is the United States, Canada, China, or Mexico, the state field is validated against a list of valid states for the respective country.</span></span> <span data-ttu-id="58f67-108">Diğer tüm ülkelerde bu test oluşmaz ve API yalnızca durumunun geçerli bir dize olduğunu denetler.</span><span class="sxs-lookup"><span data-stu-id="58f67-108">In all other countries, this test does not occur, and the API only checks that the state is a valid string.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="58f67-109">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="58f67-109">Prerequisites</span></span>

<span data-ttu-id="58f67-110">kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="58f67-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="58f67-111">Bu senaryo hem tek başına Uygulama hem de Uygulama+Kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="58f67-111">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="58f67-112">C\#</span><span class="sxs-lookup"><span data-stu-id="58f67-112">C\#</span></span>

<span data-ttu-id="58f67-113">Bir adresi doğrulamak için öncelikle yeni bir **Address** nesnesi örneği oluşturma ve bunu doğrulanması gereken adresle doldurmak.</span><span class="sxs-lookup"><span data-stu-id="58f67-113">To validate an address, first instantiate a new **Address** object and populate it with the address to validate.</span></span> <span data-ttu-id="58f67-114">Ardından **IAggregatePartner.Validations** özelliğinden **Validations** işlemlerine bir arabirim alın ve adres nesnesiyle **IsAddressValid** yöntemini arayın.</span><span class="sxs-lookup"><span data-stu-id="58f67-114">Then, retrieve an interface to **Validations** operations from the **IAggregatePartner.Validations** property, and call the **IsAddressValid** method with the address object.</span></span>

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

## <a name="java"></a><span data-ttu-id="58f67-115">Java</span><span class="sxs-lookup"><span data-stu-id="58f67-115">Java</span></span>

<span data-ttu-id="58f67-116">Bir adresi doğrulamak için öncelikle yeni bir **Address** nesnesi örneği oluşturma ve bunu doğrulanması gereken adresle doldurmak.</span><span class="sxs-lookup"><span data-stu-id="58f67-116">To validate an address, first instantiate a new **Address** object and populate it with the address to validate.</span></span> <span data-ttu-id="58f67-117">Ardından **IAggregatePartner.getValidations** işlevinden **Validations** işlemlerine bir arabirim alın ve adres nesnesiyle **isAddressValid** yöntemini arayın.</span><span class="sxs-lookup"><span data-stu-id="58f67-117">Then, retrieve an interface to **Validations** operations from the **IAggregatePartner.getValidations** function, and call the **isAddressValid** method with the address object.</span></span>

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

## <a name="powershell"></a><span data-ttu-id="58f67-118">PowerShell</span><span class="sxs-lookup"><span data-stu-id="58f67-118">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="58f67-119">Bir adresi doğrulamak için [**Test-PartnerAddress'i**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Test-PartnerAddress.md) adres parametreleri doldurulmuş şekilde yürütün.</span><span class="sxs-lookup"><span data-stu-id="58f67-119">To validate an address, execute the [**Test-PartnerAddress**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Test-PartnerAddress.md) with the address parameters populated.</span></span>

```powershell
Test-PartnerAddress -AddressLine1 '700 Bellevue Way NE' -City 'Bellevue' -Country 'US' -PostalCode '98004' -State 'WA'
```

## <a name="rest-request"></a><span data-ttu-id="58f67-120">REST isteği</span><span class="sxs-lookup"><span data-stu-id="58f67-120">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="58f67-121">İstek söz dizimi</span><span class="sxs-lookup"><span data-stu-id="58f67-121">Request syntax</span></span>

| <span data-ttu-id="58f67-122">Yöntem</span><span class="sxs-lookup"><span data-stu-id="58f67-122">Method</span></span>   | <span data-ttu-id="58f67-123">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="58f67-123">Request URI</span></span>                                                                 |
|----------|-----------------------------------------------------------------------------|
| <span data-ttu-id="58f67-124">**Yayınla**</span><span class="sxs-lookup"><span data-stu-id="58f67-124">**POST**</span></span> | <span data-ttu-id="58f67-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/validations/address HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="58f67-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/validations/address HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="58f67-126">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="58f67-126">Request headers</span></span>

<span data-ttu-id="58f67-127">Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="58f67-127">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="58f67-128">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="58f67-128">Request body</span></span>

<span data-ttu-id="58f67-129">Bu tablo, istek gövdesinde gerekli özellikleri açıklar.</span><span class="sxs-lookup"><span data-stu-id="58f67-129">This table describes the required properties in the request body.</span></span>

| <span data-ttu-id="58f67-130">Ad</span><span class="sxs-lookup"><span data-stu-id="58f67-130">Name</span></span>         | <span data-ttu-id="58f67-131">Tür</span><span class="sxs-lookup"><span data-stu-id="58f67-131">Type</span></span>   | <span data-ttu-id="58f67-132">Gerekli</span><span class="sxs-lookup"><span data-stu-id="58f67-132">Required</span></span> | <span data-ttu-id="58f67-133">Açıklama</span><span class="sxs-lookup"><span data-stu-id="58f67-133">Description</span></span>                                                |
|--------------|--------|----------|------------------------------------------------------------|
| <span data-ttu-id="58f67-134">addressline1</span><span class="sxs-lookup"><span data-stu-id="58f67-134">addressline1</span></span> | <span data-ttu-id="58f67-135">string</span><span class="sxs-lookup"><span data-stu-id="58f67-135">string</span></span> | <span data-ttu-id="58f67-136">Y</span><span class="sxs-lookup"><span data-stu-id="58f67-136">Y</span></span>        | <span data-ttu-id="58f67-137">Adresin ilk satırı.</span><span class="sxs-lookup"><span data-stu-id="58f67-137">The first line of the address.</span></span>                             |
| <span data-ttu-id="58f67-138">Addressline2</span><span class="sxs-lookup"><span data-stu-id="58f67-138">addressline2</span></span> | <span data-ttu-id="58f67-139">string</span><span class="sxs-lookup"><span data-stu-id="58f67-139">string</span></span> | <span data-ttu-id="58f67-140">N</span><span class="sxs-lookup"><span data-stu-id="58f67-140">N</span></span>        | <span data-ttu-id="58f67-141">Adresin ikinci satırı.</span><span class="sxs-lookup"><span data-stu-id="58f67-141">The second line of the address.</span></span> <span data-ttu-id="58f67-142">Bu özellik isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="58f67-142">This property is optional.</span></span> |
| <span data-ttu-id="58f67-143">city</span><span class="sxs-lookup"><span data-stu-id="58f67-143">city</span></span>         | <span data-ttu-id="58f67-144">string</span><span class="sxs-lookup"><span data-stu-id="58f67-144">string</span></span> | <span data-ttu-id="58f67-145">Y</span><span class="sxs-lookup"><span data-stu-id="58f67-145">Y</span></span>        | <span data-ttu-id="58f67-146">Şehir.</span><span class="sxs-lookup"><span data-stu-id="58f67-146">The city.</span></span>                                                  |
| <span data-ttu-id="58f67-147">state</span><span class="sxs-lookup"><span data-stu-id="58f67-147">state</span></span>        | <span data-ttu-id="58f67-148">string</span><span class="sxs-lookup"><span data-stu-id="58f67-148">string</span></span> | <span data-ttu-id="58f67-149">Y</span><span class="sxs-lookup"><span data-stu-id="58f67-149">Y</span></span>        | <span data-ttu-id="58f67-150">Durum.</span><span class="sxs-lookup"><span data-stu-id="58f67-150">The state.</span></span>                                                 |
| <span data-ttu-id="58f67-151">Postakodu</span><span class="sxs-lookup"><span data-stu-id="58f67-151">postalcode</span></span>   | <span data-ttu-id="58f67-152">string</span><span class="sxs-lookup"><span data-stu-id="58f67-152">string</span></span> | <span data-ttu-id="58f67-153">Y</span><span class="sxs-lookup"><span data-stu-id="58f67-153">Y</span></span>        | <span data-ttu-id="58f67-154">Posta kodu.</span><span class="sxs-lookup"><span data-stu-id="58f67-154">The postal code.</span></span>                                           |
| <span data-ttu-id="58f67-155">ülke</span><span class="sxs-lookup"><span data-stu-id="58f67-155">country</span></span>      | <span data-ttu-id="58f67-156">string</span><span class="sxs-lookup"><span data-stu-id="58f67-156">string</span></span> | <span data-ttu-id="58f67-157">Y</span><span class="sxs-lookup"><span data-stu-id="58f67-157">Y</span></span>        | <span data-ttu-id="58f67-158">İki karakterli ISO alfa-2 ülke kodu.</span><span class="sxs-lookup"><span data-stu-id="58f67-158">The two-character ISO alpha-2 country code.</span></span>                |

### <a name="request-example"></a><span data-ttu-id="58f67-159">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="58f67-159">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="58f67-160">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="58f67-160">REST response</span></span>

<span data-ttu-id="58f67-161">Başarılı olursa yöntemi, aşağıda gösterilen Yanıt - doğrulama başarılı örneğinde gösterildiği gibi 200 durum kodunu döndürür.</span><span class="sxs-lookup"><span data-stu-id="58f67-161">If successful, the method returns a status code 200 as demonstrated in the Response - validation succeeded example shown below.</span></span>

<span data-ttu-id="58f67-162">İstek başarısız olursa yöntem, aşağıda gösterilen Yanıt - doğrulama başarısız örneği içinde gösterildiği gibi 400 durum kodunu döndürür.</span><span class="sxs-lookup"><span data-stu-id="58f67-162">If the request fails, the method returns a status code 400 as demonstrated in the Response - validation failed example shown below.</span></span> <span data-ttu-id="58f67-163">Yanıt gövdesi, hata hakkında ek bilgiler içeren bir JSON yükü içerir.</span><span class="sxs-lookup"><span data-stu-id="58f67-163">The response body contains a JSON payload with additional information about the error.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="58f67-164">Yanıt başarı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="58f67-164">Response success and error codes</span></span>

<span data-ttu-id="58f67-165">Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="58f67-165">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="58f67-166">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="58f67-166">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="58f67-167">Tam liste için bkz. [İŞ ORTAĞı MERKEZI REST hata kodları.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="58f67-167">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response---validation-succeeded-example"></a><span data-ttu-id="58f67-168">Yanıt - doğrulama başarılı örneği</span><span class="sxs-lookup"><span data-stu-id="58f67-168">Response - validation succeeded example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 0
MS-CorrelationId: 8a853a1a-b0e6-4cb0-ae87-d6dd32ac3a0c
MS-RequestId: 0b30452a-8be2-4b8b-b25b-2d4850f4345f
MS-CV: IqhjoWVyq0Kl81dO.0
MS-ServerId: 030011719
Date: Mon, 13 Mar 2017 23:56:12 GMT
```

### <a name="response---validation-failed-example"></a><span data-ttu-id="58f67-169">Yanıt - doğrulama başarısız oldu örneği</span><span class="sxs-lookup"><span data-stu-id="58f67-169">Response - validation failed example</span></span>

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
