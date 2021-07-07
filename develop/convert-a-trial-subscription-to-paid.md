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
# <a name="convert-a-trial-subscription-to-paid-using-partner-center-apis"></a>Api'leri kullanarak deneme aboneliğini İş Ortağı Merkezi dönüştürme

Bir deneme aboneliğini ücretliye dönüştürebilirsiniz.

## <a name="prerequisites"></a>Önkoşullar

- kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md) Bu senaryo yalnızca App+User kimlik bilgileriyle kimlik doğrulamasını destekler.

- Müşteri kimliği ( `customer-tenant-id` ). Müşterinin kimliğini bilmiyorsanız bu kimliği panoda [İş Ortağı Merkezi.](https://partner.microsoft.com/dashboard) İş Ortağı Merkezi **menüsünden CSP'yi** ve ardından **Müşteriler'i seçin.** Müşteri listesinden müşteriyi ve ardından Hesap'ı **seçin.** Müşterinin Hesap sayfasında Müşteri Hesabı Bilgileri **bölümünde Microsoft** **Kimliği'ne** bakın. Microsoft Kimliği, müşteri kimliği () ile `customer-tenant-id` aynıdır.

- Etkin bir deneme aboneliği için abonelik kimliği.

- Kullanılabilir dönüştürme teklifi.

## <a name="convert-a-trial-subscription-to-a-paid-subscription-through-code"></a>Kod aracılığıyla deneme aboneliğini ücretli aboneliğe dönüştürme

Bir deneme aboneliğini ücretli bir aboneliğe dönüştürmek için öncelikle kullanılabilir deneme dönüştürmeleri koleksiyonunu alasınız. Ardından, satın almak istediğiniz dönüştürme teklifini seçmeniz gerekir.

Dönüştürme teklifleri, varsayılan olarak deneme aboneliğiyle aynı sayıda lisansa sahip olan bir miktar belirtir. [**Quantity**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.conversion.quantity) özelliğini satın almak istediğiniz lisans sayısına ayarerek bu miktarı değiştirebilirsiniz.

> [!NOTE]
> Satın alınan lisans sayısından bağımsız olarak, denemenin abonelik kimliği satın alınan lisanslar için yeniden kullanılır. Sonuç olarak, deneme sürümü kaybolur ve satın alma ile değiştirilir.

Bir deneme aboneliğini kod aracılığıyla dönüştürmek için aşağıdaki adımları kullanın:

1. Kullanılabilir abonelik işlemleri için bir arabirim alın. Müşteriyi tanımlamanız ve deneme aboneliğinin abonelik tanımlayıcısını belirtmeniz gerekir.

    ``` csharp
    var subscriptionOperations = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId);
    ```

2. Kullanılabilir dönüştürme tekliflerinin bir koleksiyonunu elde. Bu yönteme ilişkin istek/yanıt hakkında daha fazla bilgi ve ayrıntılar için [bkz. Deneme dönüştürme tekliflerinin listesini al.](get-a-list-of-trial-conversion-offers.md)

    ``` csharp
    var conversions = subscriptionOperations.Conversions.Get();
    ```

3. Bir dönüştürme teklifi seçin. Aşağıdaki kod, koleksiyonda ilk dönüştürme teklifini seçer.

    ``` csharp
    var selectedConversion = conversions.Items.ToList()[0];
    ```

4. İsteğe bağlı olarak, satın alınarak lisans sayısını belirtin. Varsayılan değer, deneme aboneliğinde lisans sayısıdır.

    ``` csharp
    selectedConversion.Quantity = 10;
    ```

5. Deneme [**aboneliğini**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.create) ücretliye dönüştürmek için Create veya [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.createasync) yöntemini çağırma.

    ``` csharp
    var convertResult = subscriptionOperations.Conversions.Create(selectedConversion);
    ```

## <a name="c"></a>C\#

Deneme aboneliğini ücretli bir aboneliğe dönüştürmek için:

1. Müşteriyi [**tanımlamak için IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini müşteri kimliğiyle birlikte kullanın.

2. Deneme aboneliği kimliğiyle [**Subscriptions.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) yöntemini çağırarak abonelik işlemlerine bir arabirim alın. Abonelik işlemleri arabirimine yönelik bir başvuru yerel değişkene kaydedin.

3. Dönüştürmeler [**üzerinde**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.conversions) kullanılabilir işlemlere bir arabirim elde etmek için Dönüştürmeler özelliğini kullanın ve ardından kullanılabilir Dönüştürme tekliflerinin koleksiyonunu almak için [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.get) veya [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.getasync) [**yöntemini**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.conversion) çağırabilirsiniz. Birini seçmeniz gerekir. Aşağıdaki örnek varsayılan olarak kullanılabilir ilk dönüştürmeyi kullanır.

4. Dönüştürmeler üzerinde kullanılabilir işlemlere bir arabirim elde etmek için, yerel değişkene kaydedilmiş abonelik işlemleri arabirimine başvuru ve [**Dönüştürmeler**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.conversions) özelliğini kullanın.

5. Deneme dönüştürmeyi denemesi için seçilen dönüştürme teklifi nesnesini [**Create**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.create) [**veya CreateAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.createasync) yöntemine iletir.

### <a name="c-example"></a>C \# örneği

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

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek söz dizimi

| Yöntem   | İstek URI'si                                                                                                                 |
|----------|-----------------------------------------------------------------------------------------------------------------------------|
| **Yayınla** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions/{subscription-id}/conversions HTTP/1.1 |

### <a name="uri-parameter"></a>URI parametresi

Müşteri ve deneme aboneliğini tanımlamak için aşağıdaki yol parametrelerini kullanın.

| Ad            | Tür   | Gerekli | Açıklama                                                     |
|-----------------|--------|----------|-----------------------------------------------------------------|
| customer-id     | string | Yes      | Müşteriyi tanımlayan GUID biçimli bir dize.           |
| subscription-id | string | Yes      | Deneme aboneliğini tanımlayan GUID biçimli bir dize. |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)

### <a name="request-body"></a>İstek gövdesi

İstek [gövdesine](conversions-resources.md#conversion) doldurulmuş bir Dönüştürme kaynağı ek gerekir.

### <a name="request-example"></a>İstek örneği

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

## <a name="rest-response"></a>REST yanıtı

Başarılı olursa yanıt gövdesi bir [ConversionResult kaynağı](conversions-resources.md#conversionresult) içerir.

#### <a name="response-success-and-error-codes"></a>Yanıt başarı ve hata kodları

Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [İş Ortağı Merkezi kodları.](error-codes.md)

#### <a name="response-example"></a>Yanıt örneği

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
