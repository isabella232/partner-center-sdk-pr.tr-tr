---
title: Microsoft Bulut Sözleşmesinin müşteri kabulünün onayını alma
description: Bu makalede, müşterinin müşteri tarafından kabulü onaylarının nasıl Microsoft Bulut Anlaşması.
ms.date: 02/12/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
aauthor: khakiali
ms.author: alikhaki
ms.openlocfilehash: eb1f9ec5a7e96984f9c458419268fb305cf13ffd44d92fd01823ad94c2fb1798
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/06/2021
ms.locfileid: "115990809"
---
# <a name="get-confirmation-of-customer-acceptance-of-microsoft-cloud-agreement"></a>Microsoft Bulut Sözleşmesinin müşteri kabulünün onayını alma

**Için geçerlidir:** İş Ortağı Merkezi

**için geçerli değildir:** İş Ortağı Merkezi 21Vianet | İş Ortağı Merkezi Microsoft Bulut Almanya için | İş Ortağı Merkezi için Microsoft Cloud for US Government

Sözleşme **kaynağı** şu anda yalnızca Microsoft İş Ortağı Merkezi bulut üzerinde kullanılabilir.

## <a name="prerequisites"></a>Önkoşullar

- İş Ortağı Merkezi .NET SDK kullanıyorsanız sürüm 1.9 veya daha yenisi gereklidir.

- İş Ortağı Merkezi Java SDK'sı kullanıyorsanız sürüm 1.8 veya daha yeni bir sürüm gereklidir.

- kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](./partner-center-authentication.md) Bu senaryo yalnızca uygulama + kullanıcı kimlik doğrulamasını destekler.

- Müşteri kimliği ( `customer-tenant-id` ). Müşterinin kimliğini bilmiyorsanız bu kimliği panoda [İş Ortağı Merkezi.](https://partner.microsoft.com/dashboard) İş Ortağı Merkezi **menüsünden CSP'yi** ve ardından **Müşteriler'i seçin.** Müşteri listesinden müşteriyi ve ardından Hesap'ı **seçin.** Müşterinin Hesap sayfasında Müşteri Hesabı Bilgileri **bölümünde Microsoft** **Kimliği'ne** bakın. Microsoft Kimliği, müşteri kimliği () ile `customer-tenant-id` aynıdır.

## <a name="net-version-14-or-newer"></a>.NET (sürüm 1.4 veya daha yenisi)

Daha önce sağlanan müşteri kabulü onaylarını almak için:

- **IAggregatePartner.Customers koleksiyonunu** kullanın ve belirtilen müşteri tanımlayıcısıyla **ById** yöntemini arayın.

- **Agreements özelliğini getirme** ve **ByAgreementType** yöntemini Microsoft Bulut Anlaşması sonuçları filtrele.

- **Get veya** **GetAsync yöntemini** çağırma.

```csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

string agreementType = "MicrosoftCloudAgreement";

var cloudAgreements = partnerOperations.Customers.ById(selectedCustomerId).Agreements.ByAgreementType(agreementType).Get();
```

Eksiksiz bir örnek, konsol test uygulaması [projesinden GetCustomerAgreements](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetCustomerAgreements.cs) [sınıfında](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) bulunabilir.

## <a name="net-version-19---113"></a>.NET (sürüm 1.9 - 1.13)

Daha önce sağlanan müşteri kabulü onaylarını almak için:

**IAggregatePartner.Customers** koleksiyonunu kullanın ve belirtilen müşterinin tanımlayıcısıyla **ById** yöntemini çağırma. Ardından **Agreements özelliğini ve** ardından **Get** veya **GetAsync yöntemlerini** çağırarak.

```csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

var agreements = partnerOperations.Customers.ById(selectedCustomerId).Agreements.Get();
```

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

Daha önce sağlanan müşteri kabulü onaylarını almak için:

**IAggregatePartner.getCustomers** işlevini kullanın ve belirtilen müşterinin tanımlayıcısıyla **byId** işlevini arayın. Ardından **getAgreements işlevini** ve ardından get işlevini **çağırarak.**

```java
// IAggregatePartner partnerOperations;
// String selectedCustomerId;

ResourceCollection<Agreement> agreements = partnerOperations.getCustomers().byId(selectedCustomerId).getAgreements().get();
```

Eksiksiz bir örnek, konsol test uygulaması [projesinden GetCustomerAgreements](https://github.com/microsoft/Partner-Center-Java-Samples/blob/master/sdk/src/main/java/com/microsoft/store/partnercenter/samples/agreements/GetCustomerAgreements.java) [sınıfında](https://github.com/Microsoft/Partner-Center-Java-Samples) bulunabilir.

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

Daha önce sağlanan müşteri kabulü onaylarını almak için:

[**Get-PartnerCustomerAgreement komutunu**](/powershell/module/partnercenter/get-partnercustomeragreement) kullanın.

```powershell
Get-PartnerCustomerAgreement -CustomerId '14876998-c0dc-46e6-9d0c-65a57a6c32ec'
```

## <a name="rest-request"></a>REST isteği

Daha önce sağlanan müşteri kabulü onaylarını almak için aşağıdaki yönergelere bakın.

İlgili sertifikasyon **bilgileriyle** yeni bir Sözleşme kaynağı oluşturun.

### <a name="request-syntax"></a>İstek söz dizimi

| Yöntem | İstek URI'si                                                                                      |
|--------|--------------------------------------------------------------------------------------------------|
| GET    | [*\{ baseURL \}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/agreements HTTP/1.1 |

#### <a name="uri-parameter"></a>URI parametresi

Onaylamakta olduğunu müşteriyi belirtmek için aşağıdaki sorgu parametresini kullanın.

| Ad             | Tür | Gerekli | Açıklama                                                                               |
|------------------|------|----------|-------------------------------------------------------------------------------------------|
| CustomerTenantId | GUID | Y        | Değer, müşteri belirtmenize olanak sağlayan GUID biçiminde bir **CustomerTenantId** değeridir. |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)

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

Başarılı olursa, bu yöntem yanıt **gövdesinde bir Anlaşma** kaynakları koleksiyonu döndürür.

### <a name="response-success-and-error-codes"></a>Yanıt başarı ve hata kodları

Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [İŞ ORTAĞı MERKEZI REST hata kodları.](error-codes.md)

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
