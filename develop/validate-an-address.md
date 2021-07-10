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
# <a name="validate-an-address"></a>Bir adresi doğrulama

**Uygulama hedefi**: Iş Ortağı Merkezi | 21Vianet tarafından işletilen iş ortağı Merkezi | Microsoft Bulut Almanya için iş ortağı Merkezi | Microsoft Cloud for US Government için iş ortağı Merkezi

Adres doğrulama API 'sini kullanarak bir adresi doğrulama.

Adres doğrulama API 'SI yalnızca müşteri profili güncelleştirmelerinin ön doğrulaması için kullanılmalıdır. Ülke Birleşik Devletler, Kanada, Çin veya Meksika olduğunda, eyalet alanının ilgili ülke için geçerli durumlar listesine göre doğrulanacağını anlamak için bunu kullanın. Diğer tüm ülkelerde, bu test oluşmaz ve API yalnızca durumun geçerli bir dize olduğunu denetler.

## <a name="prerequisites"></a>Önkoşullar

[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri. Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.

## <a name="c"></a>C\#

Bir adresi doğrulamak için önce yeni bir **Adres** nesnesi örneği oluşturun ve doğrulanacak adresle doldurun. Ardından, **ıaggregatepartner. doğrulamaları** özelliğinden **doğrulama** işlemlerine bir arabirim alın ve adres nesnesiyle **ısaddressvalid** yöntemini çağırın.

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

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek sözdizimi

| Yöntem   | İstek URI'si                                                                 |
|----------|-----------------------------------------------------------------------------|
| **Yayınla** | [*{BaseUrl}*](partner-center-rest-urls.md)/v1/validations/Address http/1.1 |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).

### <a name="request-body"></a>İstek gövdesi

Bu tabloda, istek gövdesinde gereken özellikler açıklanmaktadır.

| Ad         | Tür   | Gerekli | Açıklama                                                |
|--------------|--------|----------|------------------------------------------------------------|
| addressline1 | string | Y        | Adresin ilk satırı.                             |
| addressline2 | string | N        | Adresin ikinci satırı. Bu özellik isteğe bağlıdır. |
| city         | string | Y        | Şehir.                                                  |
| state        | string | Y        | Durum.                                                 |
| PostalCode   | string | Y        | Posta kodu.                                           |
| ülke      | string | Y        | İki karakterlik ISO Alpha-2 ülke kodu.                |

### <a name="response-details"></a>Yanıt ayrıntıları

Yanıt aşağıdaki durum iletilerinden birini döndürür:

| Durum     | Açıklama |    Döndürülen önerilen adreslerin sayısı |
|-------|---------------|-------------------|
|Doğrulanan sevk özellikli | Adres doğrulanır ve sevk edilebilir. | Tek |
|Doğrulanamayan | Adres doğrulandı. | Tek |
|Etkileşim gerekli | Önerilen adres önemli ölçüde değiştirildi ve kullanıcı onayı gerekiyor. | Tek |
|Cadde kısmi | Adreste verilen cadde kısmi ve daha fazla bilgi gerekiyor. | Birden çok — en fazla üç |
|Şirket içi kısmi | Verilen şirket içi (bina numarası, paket numarası ve diğerleri) kısmi ve daha fazla bilgi gerekiyor. | Birden çok — en fazla üç |
|Birden çok | Adreste kısmi olan birden çok alan vardır (büyük olasılıkla cadde kısmi ve şirket içi kısmı da dahil). | Birden çok — en fazla üç |
|Hiçbiri | Adres yanlış. | Hiçbiri |
|Doğrulanmamış | Adres, doğrulama işlemi aracılığıyla gönderilemedi. | Hiçbiri |

### <a name="request-example"></a>İstek örneği

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

## <a name="rest-response"></a>REST yanıtı

Başarılı olursa, yöntem yanıt gövdesinde bir **Addressvalidationresponse** nesnesi döndürür ve **http 200** durum kodudur. Aşağıda bir örnek gösterilmiştir.

### <a name="response-success-and-error-codes"></a>Yanıt başarısı ve hata kodları

Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).

### <a name="response-example"></a>Yanıt örneği

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
