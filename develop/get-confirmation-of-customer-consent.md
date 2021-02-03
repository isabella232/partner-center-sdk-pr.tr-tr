---
title: Microsoft Bulut Sözleşmesinin müşteri kabulünün onayını alma
description: Bu makalede, Microsoft Bulut sözleşmesinin müşteri kabulünün nasıl doğrulanacağı açıklanır.
ms.date: 02/12/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
aauthor: khakiali
ms.author: alikhaki
ms.openlocfilehash: d91f70cbd8bc9b8622b8d41ab9e601e2aee2cfab
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769857"
---
# <a name="get-confirmation-of-customer-acceptance-of-microsoft-cloud-agreement"></a>Microsoft Bulut Sözleşmesinin müşteri kabulünün onayını alma

**Uygulama hedefi**

- İş Ortağı Merkezi

> [!NOTE]
> **Sözleşme** kaynağı şu anda yalnızca Microsoft genel bulutundaki Iş Ortağı Merkezi tarafından desteklenmektedir. Şunları yapmak için geçerli değildir:
>
> - 21Vianet tarafından çalıştırılan iş ortağı Merkezi
> - Microsoft Bulut Almanya için İş Ortağı Merkezi
> - Microsoft Cloud for US Government için İş Ortağı Merkezi

## <a name="prerequisites"></a>Önkoşullar

- Iş ortağı merkezi .NET SDK kullanıyorsanız sürüm 1,9 veya daha yeni bir sürümü gereklidir.

- Iş ortağı merkezi Java SDK 'sını kullanıyorsanız sürüm 1,8 veya daha yeni bir sürümü gereklidir.

- [Iş ortağı merkezi kimlik doğrulamasında](./partner-center-authentication.md)açıklandığı gibi kimlik bilgileri. Bu senaryo yalnızca uygulama + kullanıcı kimlik doğrulamasını destekler.

- Bir müşteri KIMLIĞI ( `customer-tenant-id` ). Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz. Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin. Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin. Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın. Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .

## <a name="net-version-14-or-newer"></a>.NET (sürüm 1,4 veya üzeri)

Daha önce sağlanmış olan müşteri kabulünün onayını almak için:

- Belirtilen müşteri tanımlayıcısıyla **ıaggregatepartner. Customers** koleksiyonunu ve Call **byıd** metodunu kullanın.

- **Byagreementtype** metodunu çağırarak **anlaşmalar** özelliğini getirin ve sonuçları Microsoft bulut sözleşmeye filtreleyin.

- **Get** veya **GetAsync** metodunu çağırın.

```csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

string agreementType = "MicrosoftCloudAgreement";

var cloudAgreements = partnerOperations.Customers.ById(selectedCustomerId).Agreements.ByAgreementType(agreementType).Get();
```

Tüm örnek, [konsol test uygulaması](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) projesinden [getcustomersözleşmeleri](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetCustomerAgreements.cs) sınıfında bulunabilir.

## <a name="net-version-19---113"></a>.NET (sürüm 1,9-1,13)

Daha önce sağlanmış olan müşteri kabulünün onayını almak için:

**Iaggregatepartner. Customers** koleksiyonunu kullanın ve **byıd** metodunu belirtilen müşterinin tanımlayıcısıyla çağırın. Ardından, **Get** veya **GetAsync** yöntemlerini çağırarak **anlaşmalar** özelliğini alın.

```csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

var agreements = partnerOperations.Customers.ById(selectedCustomerId).Agreements.Get();
```

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

Daha önce sağlanmış olan müşteri kabulünün onayını almak için:

**Iaggregatepartner. getCustomers** işlevini kullanın ve belirtilen müşterinin tanımlayıcısına sahip **byıd** işlevini çağırın. Ardından, **Get** Işlevini çağırarak **getagreements** işlevini alın.

```java
// IAggregatePartner partnerOperations;
// String selectedCustomerId;

ResourceCollection<Agreement> agreements = partnerOperations.getCustomers().byId(selectedCustomerId).getAgreements().get();
```

Tüm örnek, [konsol test uygulaması](https://github.com/Microsoft/Partner-Center-Java-Samples) projesinden [getcustomersözleşmeleri](https://github.com/microsoft/Partner-Center-Java-Samples/blob/master/sdk/src/main/java/com/microsoft/store/partnercenter/samples/agreements/GetCustomerAgreements.java) sınıfında bulunabilir.

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

Daha önce sağlanmış olan müşteri kabulünün onayını almak için:

[**Get-PartnerCustomerAgreement**](/powershell/module/partnercenter/get-partnercustomeragreement) komutunu kullanın.

```powershell
Get-PartnerCustomerAgreement -CustomerId '14876998-c0dc-46e6-9d0c-65a57a6c32ec'
```

## <a name="rest-request"></a>REST isteği

Daha önce sağlanmış olan müşteri kabulünün onayını almak için aşağıdaki yönergelere bakın.

İlgili sertifika bilgileriyle yeni bir **anlaşma** kaynağı oluşturun.

### <a name="request-syntax"></a>İstek sözdizimi

| Yöntem | İstek URI'si                                                                                      |
|--------|--------------------------------------------------------------------------------------------------|
| GET    | [*\{ BaseUrl \}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/sözleşmeleri http/1.1 |

#### <a name="uri-parameter"></a>URI parametresi

Onayladığınız müşteriyi belirtmek için aşağıdaki sorgu parametresini kullanın.

| Ad             | Tür | Gerekli | Açıklama                                                                               |
|------------------|------|----------|-------------------------------------------------------------------------------------------|
| CustomerTenantId | GUID | Y        | Değer, bir müşteriyi belirtmenizi sağlayan bir GUID biçimli **Customertenantıd** 'dir. |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).

### <a name="request-body"></a>İstek gövdesi

Yok.

### <a name="request-example"></a>İstek örneği

```http
GET https://api.partnercenter.microsoft.com/v1/customers/14876998-c0dc-46e6-9d0c-65a57a6c32ec/agreements HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

## <a name="rest-response"></a>REST yanıtı

Başarılı olursa, bu yöntem yanıt gövdesinde **anlaşma** kaynaklarının bir koleksiyonunu döndürür.

### <a name="response-success-and-error-codes"></a>Yanıt başarısı ve hata kodları

Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).

### <a name="response-example"></a>Yanıt örneği

```http
HTTP/1.1 200 OK
Content-Length: 620
Content-Type: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
{
    "totalCount": 2,
    "items":
    [
        {
            "primaryContact":
            {
                "firstName":"Tania",
                "lastName":"Carr",
                "email":"SomeEmail@Outlook.com"
                "phoneNumber":"1234567890"
            },
            "templateId":"998b88de-aa99-4388-a42c-1b3517d49490",
            "dateAgreed":"2018-07-28T00:00:00",
            "type":"MicrosoftCloudAgreement",
            "agreementLink":"https://docs.microsoft.com/partner-center/agreements"
        },
        {
            "primaryContact":
            {
                "firstName":"Tania",
                "lastName":"Carr",
                "email":"SomeEmail@Outlook.com"
                "phoneNumber:"1234567890"
            },
            "templateId":"998b88de-aa99-4388-a42c-1b3517d49490",
            "dateAgreed":"2017-08-01T00:00:00",
            "type":"MicrosoftCloudAgreement",
            "agreementLink":"https://docs.microsoft.com/partner-center/agreements"
        }
    ]
}
```
